---
title: parquet编码定义
author: fatkun
type: post
date: 2016-11-13T12:29:49+00:00
url: /2016/11/parquet-encoding-definitions.html
duoshuo_thread_id:
  - 6352429012400210689
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:639:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="other" style="font-family:monospace;">dec value: 0   1   2   3   4   5   6   7
    bit value: 000 001 010 011 100 101 110 111
    bit label: ABC DEF GHI JKL MNO PQR STU VWX
    编码后
    bit value: 10001000 11000110 11111010
    bit label: HIDEFABC RMNOJKLG VWXSTUPQ</pre></td></tr></table><p class="theCode" style="display:none;">dec value: 0   1   2   3   4   5   6   7
    bit value: 000 001 010 011 100 101 110 111
    bit label: ABC DEF GHI JKL MNO PQR STU VWX
    编码后
    bit value: 10001000 11000110 11111010
    bit label: HIDEFABC RMNOJKLG VWXSTUPQ</p></div>
    ";}
categories:
  - hadoop
tags:
  - hdfs
  - parquet
  - 文件格式

---
主要是翻译https://github.com/Parquet/parquet-format/blob/master/Encodings.md内容，没有完整翻译，有些地方没有理解，可能有理解错的地方。
## Plain: (PLAIN = 0)

如果没有更高效的编码方式就采用这种方式存储
BOOLEAN: Bit Packed, LSB first  
INT32: 4 bytes 小端存储  
INT64: 8 bytes 小端存储  
INT96: 12 bytes 小端存储  
FLOAT: 4 bytes IEEE 小端存储  
DOUBLE: 8 bytes IEEE 小端存储  
BYTE_ARRAY: 4 bytes 小端存储字符数组长度，接着是字符字节  
FIXED\_LEN\_BYTE_ARRAY: 纯字符字节（这个应该是固定长度的字符）
使用小端存储是因为存储快（未确认，见整型编码调研）
## Dictionary Encoding (PLAIN\_DICTIONARY = 2) 字典编码（已过时，官方文档没更新，使用RLE\_DICTIONARY代替）

对列的内容构建一个字典，字典会存储在每一个column chunk的dictionary page,内容页都存储为int类型使用RLE/Bit-Packing Hybrid（变长长度编码/Bit-Packing混合）编码  
如果字典太大，不管是因为大小还是排重值过多，这种编码会退化为plain编码。  
Dictionary page会在每个column chunk的开头，接着是data page。
Dictionary page 格式：使用plain编码存储，按字典的顺序  
Data page 格式：使用1bytes存储位宽（bit width），最大位宽32bit。接着是使用RLE/Bit packed来存储指向数据的ID。  
字典编码举例：构造字典AAA(1) BBB(2),那存储AAABBBAAA就变成：字典内容加上121
## Run Length Encoding / Bit-Packing Hybrid (RLE = 3)  变长长度编码/Bit-Packing混合

场景：用于存储重复的数据
存储格式
> rle-bit-packed-hybrid: <length> <encoded-data>  
> length := <encoded-data> 的长度，用4bytes小端存储  
> encoded-data := <run>*  
> run := <bit-packed-run> | <rle-run>  
> bit-packed-run := <bit-packed-header> <bit-packed-values>  
> bit-packed-header := varint-encode(<bit-pack-count> << 1 | 1) //左移一位，最后一位补1，用来区分RLE，varint-encode搜索vlq编码  
> // bit-pack 总是每次压缩8个值，所以只用存储除以8  
> bit-pack-count := (number of values in this run) / 8  
> bit-packed-values := \*see 1 below\*  
> rle-run := <rle-header> <repeated-value>  
> rle-header := varint-encode( (number of times repeated) << 1) // 重复的次数  
> repeated-value := value that is repeated, using a fixed-width of round-up-to-next-byte(bit-width) // 重复的内容，round-up-to-next-byte没看懂
以 0 至 7 这八个数字为例子
<pre lang="other" escaped="true">dec value: 0   1   2   3   4   5   6   7
bit value: 000 001 010 011 100 101 110 111
bit label: ABC DEF GHI JKL MNO PQR STU VWX
编码后
bit value: 10001000 11000110 11111010
bit label: HIDEFABC RMNOJKLG VWXSTUPQ</pre>
&nbsp;
和下面的Bit-packed (Deprecated)存储顺序不一样，这个是从least significant to most significant（从低位到高位）存储，但是值的位顺序不变  
注意看bit label
为什么用这种顺序？看起来是像对小端硬件的优化。
> The reason for this packing order is to have fewer word-boundaries on little-endian hardware when deserializing more than one byte at at time. This is because 4 bytes can be read into a 32 bit register (or 8 bytes into a 64 bit register) and values can be unpacked just by shifting and ORing with a mask. (to make this optimization work on a big-endian machine, you would have to use the ordering used in the deprecated bit-packing encoding)
varint-encode() is ULEB-128 encoding, 搜索vlq编码
&nbsp;
## Bit-packed (Deprecated) (BIT_PACKED = 4)

已被Run Length Encoding / Bit-Packing Hybrid代替  
举例说明，假如要存储0,1,2,3,4,5,6,7这8个数字，用plain的方式来存储是4bytes一个数字，总共 4 \* 8 \* 8 = 256位。现在采用位编码来存储上面的值，上面最大的数字7用位来表示是：00000000 00000000 00000000 00000111，它的有效位是111，只要用3bit就能存储所有比它小的值，8个数字共占用空间3*8=24bit。
<pre>dec value: 0   1   2   3   4   5   6   7
bit value: 000 001 010 011 100 101 110 111
bit label: ABC DEF GHI JKL MNO PQR STU VWX

bit value: 00000101 00111001 01110111
bit label: ABCDEFGH IJKLMNOP QRSTUVWX</pre>
bit label是用来标识上面的每一位的具体位置。
## Delta Encoding (DELTA\_BINARY\_PACKED = 5)差分编码

支持类型: INT32, INT64
Delta Encoding由header+blocks of delta encoded values构成。每个block里面有多个miniblock，每一个miniblock有不同的bit width来压缩（binary packed）。 When there are not enough values to encode a full block we pad with zeros (added to the frame of reference)
header如下：
`<block size in values> <number of miniblocks in a block> <total value count> <first value><br />
` 
  * block size：一个乘以128用VLQ int存储的值（不清楚这个值怎么算）
  * the miniblock count per block：miniblock的个数，用block size除以它可以算出每个block大小。一个乘以32用VLQ int存储的值
  * total value count：VLQ int存储
  * first value：zigzag VLQ int存储
每一个block包含
    <min delta> <list of bitwidths of miniblocks> <miniblocks>
  * min delta：最小的差值（VLQ int），计算最小的差值是为了bit packing的时候都是正数
  * bitwidth of each block用1 byte存储
  * miniblocks：是一组根据前面指定bit width的bit packed 数字
有多个block是因为可以有多个基准值
### 如何计算？

  1. 计算相邻的差值
  2. 使用zigzag VLQ int编码第一个值
  3. 每一个block里计算参照值(frame of reference)（最小的那个差异值），这个保证每个差量都是正数
  4. 使用VLQ int编码参照值，然后接着的是bit packed 的差异量(每一个减去参考值)
如果这个block只有一个值，第2,3步省略
#### 例子1

1, 2, 3, 4, 5
第1步后，计算每个数字和前一个数字的差值
1, 1, 1, 1
最小的差异值是1，第二步后
0, 0, 0, 0
最终编码的数据为：
header: 8 (block size), 1 (miniblock count), 5 (value count), 1 (first value)
block 1 (minimum delta), 0 (bitwidth), (no data needed for bitwidth 0)
#### 例子2

7, 5, 3, 1, 2, 3, 4, 5，差异值为
-2, -2, -2, 1, 1, 1, 1
最小差异值为-2，每个差异值减去这个值后
0, 0, 0, 3, 3, 3, 3
最终编码的数据为：
header: 8 (block size), 1 (miniblock count), 8 (value count), 7 (first value)
block: 0 (minimum delta), 2 (bitwidth), 000000111111b (0,0,0,3,3,3 packed on 2 bits)
（这里不理解为什么minimum delta是0，block size也不清楚为什么是8）
### 特性

有点像[RLE/bit-packing][1]，但是[RLE/bit-packing][1]在一个page里面使用单一的bit width。差分算法使用多个minblocks，可以有不同的bit width，对数值大小变化没那么敏感。如果在一段数据里面都是同一个值，这种算法只需要存储header就行了，不用存储数据（见例子1），这也是一种RLE编码。
&nbsp;
## Delta-length byte array: (DELTA\_LENGTH\_BYTE_ARRAY = 6)

支持类型: BYTE_ARRAY
这个编码比PLAIN的byte array好
存储方式，使用差分编码（DELTA\_BINARY\_PACKED）的方式来存储每个字符串的长度，接着就是每个字符串拼接起来。
这样做的好处是节省了记录长度的空间，以及对压缩好一些（不用在数据中间插入字符长度）
例子：
&#8220;Hello&#8221;, &#8220;World&#8221;, &#8220;Foobar&#8221;, &#8220;ABCDEF&#8221; -》DeltaEncoding(5, 5, 6, 6) &#8220;HelloWorldFoobarABCDEF&#8221;
## Delta Strings: (DELTA\_BYTE\_ARRAY = 7)

支持类型: BYTE_ARRAY，适用于字符较多相似的字符数组
使用incremental encoding(<http://en.wikipedia.org/wiki/Incremental_encoding>)编码，用DELTA\_BINARY\_PACKED编码来存储prefix lengths（前缀的长度），然后跟着用DELTA\_LENGTH\_BYTE_ARRAY编码的字节数组
例子：
&#8220;cat&#8221; &#8220;catlog&#8221; &#8220;abc&#8221; &#8220;abd&#8221; &#8220;add&#8221;
使用incremental encoding，前面是prefix lengths，表示和前一个字符串相同的字符串有多少
&#8220;0 cat&#8221;   &#8220;3 log&#8221;  &#8220;0 abc&#8221;  &#8220;2 d&#8221; &#8220;1dd&#8221;
最终存储
DELTA\_BINARY\_PACKED(0, 3, 0, 2, 1) DeltaEncoding(3, 3, 3, 1, 2) &#8220;catlogabcddd&#8221;
&nbsp;
## 参考

https://github.com/Parquet/parquet-format/blob/master/Encodings.md  
https://github.com/apache/parquet-format
深入分析Parquet列式存储格式 <http://www.infoq.com/cn/articles/in-depth-analysis-of-parquet-column-storage-format>  
整型编码调研 [https://github.com/sjtufighter/&#8212;-Data&#8212;Storage&#8211;/blob/master/encodingDetails.md][2]  
VLQ(Variable-length quantity) 编码规则 <http://blog.allenm.me/2012/12/base64-vlq-encoding/>

 [1]: https://github.com/Parquet/parquet-format/blob/master/Encodings.md#RLE
 [2]: https://github.com/sjtufighter/----Data---Storage--/blob/master/encodingDetails.md