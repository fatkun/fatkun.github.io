---
title: Hive更改输入输出文件格式
author: fatkun
type: post
date: 2013-06-04T07:52:01+00:00
url: /2013/06/alter-table-partition-file-format.html
duoshuo_thread_id:
  - 6300410023990264577
categories:
  - hive
tags:
  - hive

---
文档：<https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL>  
ALTER TABLE table\_name [PARTITION partitionSpec] SET FILEFORMAT file\_format
分区和表都会存储了文件格式，都要改过来才正确。。
例子：
ALTER TABLE foo SET FILEFORMAT  
INPUTFORMAT &#8220;com.hadoop.mapred.DeprecatedLzoTextInputFormat&#8221;  
OUTPUTFORMAT &#8220;org.apache.hadoop.hive.ql.io.HiveIgnoreKeyTextOutputFormat&#8221;;
ALTER TABLE foo PARTITION (pt=&#8217;2013-06-04&#8242;) SET FILEFORMAT  
INPUTFORMAT &#8220;com.hadoop.mapred.DeprecatedLzoTextInputFormat&#8221;  
OUTPUTFORMAT &#8220;org.apache.hadoop.hive.ql.io.HiveIgnoreKeyTextOutputFormat&#8221;;
也可以直接改metastore数据库，但要注意hive服务端可能有cache（默认是开了level2 cache），不知道会不会影响。
更改SD表  
UPDATE SDS SET INPUT_FORMAT=&#8217;com.hadoop.mapred.DeprecatedLzoTextInputFormat&#8217;;