---
title: glusterFs性能评测
author: fatkun
type: post
date: -001-11-30T00:00:00+00:00
draft: true
url: /?p=2206
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:11354:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #666666; font-style: italic;">#./iozone -w -c -e -i 0 -+n -C -r 64k -s 1g -t 8 -F /mnt/gfs/f{0,1,2,3,4,5,6,7,8}.ioz</span>
    Iozone: Performance Test of File I<span style="color: #000000; font-weight: bold;">/</span>O
    Version <span style="color: #007800;">$Revision</span>: <span style="color: #000000;">3.471</span> $
    Compiled <span style="color: #000000; font-weight: bold;">for</span> <span style="color: #000000;">64</span> bit mode.
    Build: linux-AMD64
    &nbsp;
    Contributors:William Norcott, Don Capps, Isom Crawford, Kirby Collins
    Al Slater, Scott Rhine, Mike Wisner, Ken Goss
    Steve Landherr, Brad Smith, Mark Kelly, Dr. Alain CYR,
    Randy Dunlap, Mark Montague, Dan Million, Gavin Brebner,
    Jean-Marc Zucconi, Jeff Blomberg, Benny Halevy, Dave Boone,
    Erik Habbinga, Kris Strecker, Walter Wong, Joshua Root,
    Fabrice Bacchella, Zhenghua Xue, Qin Li, Darren Sawyer,
    Vangel Bojaxhi, Ben England, Vikentsi Lapa,
    Alexey Skidanov.
    &nbsp;
    Run began: Sun Mar <span style="color: #000000;">18</span> <span style="color: #000000;">17</span>:<span style="color: #000000;">45</span>:<span style="color: #000000;">52</span> <span style="color: #000000;">2018</span>
    &nbsp;
    Setting no_unlink
    Include close <span style="color: #000000; font-weight: bold;">in</span> <span style="color: #c20cb9; font-weight: bold;">write</span> timing
    Include fsync <span style="color: #000000; font-weight: bold;">in</span> <span style="color: #c20cb9; font-weight: bold;">write</span> timing
    No retest option selected
    Record Size <span style="color: #000000;">64</span> kB
    File <span style="color: #c20cb9; font-weight: bold;">size</span> <span style="color: #000000; font-weight: bold;">set</span> to <span style="color: #000000;">1048576</span> kB
    Command line used: .<span style="color: #000000; font-weight: bold;">/</span>iozone <span style="color: #660033;">-w</span> <span style="color: #660033;">-c</span> <span style="color: #660033;">-e</span> <span style="color: #660033;">-i</span> <span style="color: #000000;">0</span> -+n <span style="color: #660033;">-C</span> <span style="color: #660033;">-r</span> 64k <span style="color: #660033;">-s</span> 1g <span style="color: #660033;">-t</span> <span style="color: #000000;">8</span> <span style="color: #660033;">-F</span> <span style="color: #000000; font-weight: bold;">/</span>mnt<span style="color: #000000; font-weight: bold;">/</span>gfs<span style="color: #000000; font-weight: bold;">/</span>f0.ioz <span style="color: #000000; font-weight: bold;">/</span>mnt<span style="color: #000000; font-weight: bold;">/</span>gfs<span style="color: #000000; font-weight: bold;">/</span>f1.ioz <span style="color: #000000; font-weight: bold;">/</span>mnt<span style="color: #000000; font-weight: bold;">/</span>gfs<span style="color: #000000; font-weight: bold;">/</span>f2.ioz <span style="color: #000000; font-weight: bold;">/</span>mnt<span style="color: #000000; font-weight: bold;">/</span>gfs<span style="color: #000000; font-weight: bold;">/</span>f3.ioz <span style="color: #000000; font-weight: bold;">/</span>mnt<span style="color: #000000; font-weight: bold;">/</span>gfs<span style="color: #000000; font-weight: bold;">/</span>f4.ioz <span style="color: #000000; font-weight: bold;">/</span>mnt<span style="color: #000000; font-weight: bold;">/</span>gfs<span style="color: #000000; font-weight: bold;">/</span>f5.ioz <span style="color: #000000; font-weight: bold;">/</span>mnt<span style="color: #000000; font-weight: bold;">/</span>gfs<span style="color: #000000; font-weight: bold;">/</span>f6.ioz <span style="color: #000000; font-weight: bold;">/</span>mnt<span style="color: #000000; font-weight: bold;">/</span>gfs<span style="color: #000000; font-weight: bold;">/</span>f7.ioz <span style="color: #000000; font-weight: bold;">/</span>mnt<span style="color: #000000; font-weight: bold;">/</span>gfs<span style="color: #000000; font-weight: bold;">/</span>f8.ioz
    Output is <span style="color: #000000; font-weight: bold;">in</span> kBytes<span style="color: #000000; font-weight: bold;">/</span>sec
    Time Resolution = <span style="color: #000000;">0.000001</span> seconds.
    Processor cache <span style="color: #c20cb9; font-weight: bold;">size</span> <span style="color: #000000; font-weight: bold;">set</span> to <span style="color: #000000;">1024</span> kBytes.
    Processor cache line <span style="color: #c20cb9; font-weight: bold;">size</span> <span style="color: #000000; font-weight: bold;">set</span> to <span style="color: #000000;">32</span> bytes.
    File stride <span style="color: #c20cb9; font-weight: bold;">size</span> <span style="color: #000000; font-weight: bold;">set</span> to <span style="color: #000000;">17</span> <span style="color: #000000; font-weight: bold;">*</span> record size.
    Throughput <span style="color: #7a0874; font-weight: bold;">test</span> with <span style="color: #000000;">8</span> processes
    Each process writes a <span style="color: #000000;">1048576</span> kByte <span style="color: #c20cb9; font-weight: bold;">file</span> <span style="color: #000000; font-weight: bold;">in</span> <span style="color: #000000;">64</span> kByte records
    &nbsp;
    &nbsp;
    Children see throughput <span style="color: #000000; font-weight: bold;">for</span> <span style="color: #000000;">8</span> initial writers = <span style="color: #000000;">134187.12</span> kB<span style="color: #000000; font-weight: bold;">/</span>sec
    Parent sees throughput <span style="color: #000000; font-weight: bold;">for</span> <span style="color: #000000;">8</span> initial writers = <span style="color: #000000;">129757.45</span> kB<span style="color: #000000; font-weight: bold;">/</span>sec
    Min throughput per process = <span style="color: #000000;">16315.78</span> kB<span style="color: #000000; font-weight: bold;">/</span>sec 
    Max throughput per process = <span style="color: #000000;">17234.54</span> kB<span style="color: #000000; font-weight: bold;">/</span>sec
    Avg throughput per process = <span style="color: #000000;">16773.39</span> kB<span style="color: #000000; font-weight: bold;">/</span>sec
    Min xfer = <span style="color: #000000;">927104.00</span> kB
    Child<span style="color: #7a0874; font-weight: bold;">&#91;</span><span style="color: #000000;">0</span><span style="color: #7a0874; font-weight: bold;">&#93;</span> xfer count = <span style="color: #000000;">992256.00</span> kB, Throughput = <span style="color: #000000;">17234.54</span> kB<span style="color: #000000; font-weight: bold;">/</span>sec
    Child<span style="color: #7a0874; font-weight: bold;">&#91;</span><span style="color: #000000;">1</span><span style="color: #7a0874; font-weight: bold;">&#93;</span> xfer count = <span style="color: #000000;">1013760.00</span> kB, Throughput = <span style="color: #000000;">16946.16</span> kB<span style="color: #000000; font-weight: bold;">/</span>sec
    Child<span style="color: #7a0874; font-weight: bold;">&#91;</span><span style="color: #000000;">2</span><span style="color: #7a0874; font-weight: bold;">&#93;</span> xfer count = <span style="color: #000000;">976576.00</span> kB, Throughput = <span style="color: #000000;">16324.60</span> kB<span style="color: #000000; font-weight: bold;">/</span>sec
    Child<span style="color: #7a0874; font-weight: bold;">&#91;</span><span style="color: #000000;">3</span><span style="color: #7a0874; font-weight: bold;">&#93;</span> xfer count = <span style="color: #000000;">1048576.00</span> kB, Throughput = <span style="color: #000000;">17152.88</span> kB<span style="color: #000000; font-weight: bold;">/</span>sec
    Child<span style="color: #7a0874; font-weight: bold;">&#91;</span><span style="color: #000000;">4</span><span style="color: #7a0874; font-weight: bold;">&#93;</span> xfer count = <span style="color: #000000;">927104.00</span> kB, Throughput = <span style="color: #000000;">16315.78</span> kB<span style="color: #000000; font-weight: bold;">/</span>sec
    Child<span style="color: #7a0874; font-weight: bold;">&#91;</span><span style="color: #000000;">5</span><span style="color: #7a0874; font-weight: bold;">&#93;</span> xfer count = <span style="color: #000000;">1006208.00</span> kB, Throughput = <span style="color: #000000;">16819.89</span> kB<span style="color: #000000; font-weight: bold;">/</span>sec
    Child<span style="color: #7a0874; font-weight: bold;">&#91;</span><span style="color: #000000;">6</span><span style="color: #7a0874; font-weight: bold;">&#93;</span> xfer count = <span style="color: #000000;">1031296.00</span> kB, Throughput = <span style="color: #000000;">16832.92</span> kB<span style="color: #000000; font-weight: bold;">/</span>sec
    Child<span style="color: #7a0874; font-weight: bold;">&#91;</span><span style="color: #000000;">7</span><span style="color: #7a0874; font-weight: bold;">&#93;</span> xfer count = <span style="color: #000000;">1012352.00</span> kB, Throughput = <span style="color: #000000;">16560.34</span> kB<span style="color: #000000; font-weight: bold;">/</span>sec</pre></td></tr></table><p class="theCode" style="display:none;">#./iozone -w -c -e -i 0 -+n -C -r 64k -s 1g -t 8 -F /mnt/gfs/f{0,1,2,3,4,5,6,7,8}.ioz
    Iozone: Performance Test of File I/O
    Version $Revision: 3.471 $
    Compiled for 64 bit mode.
    Build: linux-AMD64
    
    Contributors:William Norcott, Don Capps, Isom Crawford, Kirby Collins
    Al Slater, Scott Rhine, Mike Wisner, Ken Goss
    Steve Landherr, Brad Smith, Mark Kelly, Dr. Alain CYR,
    Randy Dunlap, Mark Montague, Dan Million, Gavin Brebner,
    Jean-Marc Zucconi, Jeff Blomberg, Benny Halevy, Dave Boone,
    Erik Habbinga, Kris Strecker, Walter Wong, Joshua Root,
    Fabrice Bacchella, Zhenghua Xue, Qin Li, Darren Sawyer,
    Vangel Bojaxhi, Ben England, Vikentsi Lapa,
    Alexey Skidanov.
    
    Run began: Sun Mar 18 17:45:52 2018
    
    Setting no_unlink
    Include close in write timing
    Include fsync in write timing
    No retest option selected
    Record Size 64 kB
    File size set to 1048576 kB
    Command line used: ./iozone -w -c -e -i 0 -+n -C -r 64k -s 1g -t 8 -F /mnt/gfs/f0.ioz /mnt/gfs/f1.ioz /mnt/gfs/f2.ioz /mnt/gfs/f3.ioz /mnt/gfs/f4.ioz /mnt/gfs/f5.ioz /mnt/gfs/f6.ioz /mnt/gfs/f7.ioz /mnt/gfs/f8.ioz
    Output is in kBytes/sec
    Time Resolution = 0.000001 seconds.
    Processor cache size set to 1024 kBytes.
    Processor cache line size set to 32 bytes.
    File stride size set to 17 * record size.
    Throughput test with 8 processes
    Each process writes a 1048576 kByte file in 64 kByte records
    
    
    Children see throughput for 8 initial writers = 134187.12 kB/sec
    Parent sees throughput for 8 initial writers = 129757.45 kB/sec
    Min throughput per process = 16315.78 kB/sec 
    Max throughput per process = 17234.54 kB/sec
    Avg throughput per process = 16773.39 kB/sec
    Min xfer = 927104.00 kB
    Child[0] xfer count = 992256.00 kB, Throughput = 17234.54 kB/sec
    Child[1] xfer count = 1013760.00 kB, Throughput = 16946.16 kB/sec
    Child[2] xfer count = 976576.00 kB, Throughput = 16324.60 kB/sec
    Child[3] xfer count = 1048576.00 kB, Throughput = 17152.88 kB/sec
    Child[4] xfer count = 927104.00 kB, Throughput = 16315.78 kB/sec
    Child[5] xfer count = 1006208.00 kB, Throughput = 16819.89 kB/sec
    Child[6] xfer count = 1031296.00 kB, Throughput = 16832.92 kB/sec
    Child[7] xfer count = 1012352.00 kB, Throughput = 16560.34 kB/sec</p></div>
    ";}
categories:
  - 未分类
tags:
  - glusterFs

---
<pre lang="bash" escaped="true">#./iozone -w -c -e -i 0 -+n -C -r 64k -s 1g -t 8 -F /mnt/gfs/f{0,1,2,3,4,5,6,7,8}.ioz
Iozone: Performance Test of File I/O
Version $Revision: 3.471 $
Compiled for 64 bit mode.
Build: linux-AMD64

Contributors:William Norcott, Don Capps, Isom Crawford, Kirby Collins
Al Slater, Scott Rhine, Mike Wisner, Ken Goss
Steve Landherr, Brad Smith, Mark Kelly, Dr. Alain CYR,
Randy Dunlap, Mark Montague, Dan Million, Gavin Brebner,
Jean-Marc Zucconi, Jeff Blomberg, Benny Halevy, Dave Boone,
Erik Habbinga, Kris Strecker, Walter Wong, Joshua Root,
Fabrice Bacchella, Zhenghua Xue, Qin Li, Darren Sawyer,
Vangel Bojaxhi, Ben England, Vikentsi Lapa,
Alexey Skidanov.

Run began: Sun Mar 18 17:45:52 2018

Setting no_unlink
Include close in write timing
Include fsync in write timing
No retest option selected
Record Size 64 kB
File size set to 1048576 kB
Command line used: ./iozone -w -c -e -i 0 -+n -C -r 64k -s 1g -t 8 -F /mnt/gfs/f0.ioz /mnt/gfs/f1.ioz /mnt/gfs/f2.ioz /mnt/gfs/f3.ioz /mnt/gfs/f4.ioz /mnt/gfs/f5.ioz /mnt/gfs/f6.ioz /mnt/gfs/f7.ioz /mnt/gfs/f8.ioz
Output is in kBytes/sec
Time Resolution = 0.000001 seconds.
Processor cache size set to 1024 kBytes.
Processor cache line size set to 32 bytes.
File stride size set to 17 * record size.
Throughput test with 8 processes
Each process writes a 1048576 kByte file in 64 kByte records


Children see throughput for 8 initial writers = 134187.12 kB/sec
Parent sees throughput for 8 initial writers = 129757.45 kB/sec
Min throughput per process = 16315.78 kB/sec 
Max throughput per process = 17234.54 kB/sec
Avg throughput per process = 16773.39 kB/sec
Min xfer = 927104.00 kB
Child[0] xfer count = 992256.00 kB, Throughput = 17234.54 kB/sec
Child[1] xfer count = 1013760.00 kB, Throughput = 16946.16 kB/sec
Child[2] xfer count = 976576.00 kB, Throughput = 16324.60 kB/sec
Child[3] xfer count = 1048576.00 kB, Throughput = 17152.88 kB/sec
Child[4] xfer count = 927104.00 kB, Throughput = 16315.78 kB/sec
Child[5] xfer count = 1006208.00 kB, Throughput = 16819.89 kB/sec
Child[6] xfer count = 1031296.00 kB, Throughput = 16832.92 kB/sec
Child[7] xfer count = 1012352.00 kB, Throughput = 16560.34 kB/sec</pre>
&nbsp;
&nbsp;
## 参考

http://wiki.stoney-cloud.org/wiki/GlusterFS_Benchmark
[glusterfs部署 http://jaminzhang.github.io/glusterfs/GlusterFS-02-Deploy-and-Config/][1]
Error: /home11/gluster_data is already part of a volume
https://joejulian.name/post/glusterfs-path-or-a-prefix-of-it-is-already-part-of-a-volume/
&nbsp;

 [1]: http://jaminzhang.github.io/glusterfs/GlusterFS-02-Deploy-and-Config/