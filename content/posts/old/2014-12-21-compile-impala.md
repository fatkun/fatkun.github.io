---
title: 编译impala2.0.0
author: fatkun
type: post
date: 2014-12-21T08:50:16+00:00
url: /2014/12/compile-impala.html
duoshuo_thread_id:
  - 6300410881255670529
wp-syntax-cache-content:
  - |
    a:7:{i:1;s:556:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;">rpm <span style="color: #660033;">-e</span> <span style="color: #000000; font-weight: bold;">`</span>rpm <span style="color: #660033;">-qa</span><span style="color: #000000; font-weight: bold;">|</span><span style="color: #c20cb9; font-weight: bold;">grep</span> boost<span style="color: #000000; font-weight: bold;">`</span></pre></td></tr></table><p class="theCode" style="display:none;">rpm -e `rpm -qa|grep boost`</p></div>
    ";i:2;s:1959:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #7a0874; font-weight: bold;">cd</span> boost_1_46_1
    <span style="color: #c20cb9; font-weight: bold;">sh</span> .<span style="color: #000000; font-weight: bold;">/</span>bootstrap.sh
    <span style="color: #666666; font-style: italic;">#注意要加上 cxxflags=-fPIC 参数，否则后面编译失败</span>
    .<span style="color: #000000; font-weight: bold;">/</span>bjam <span style="color: #660033;">--libdir</span>=<span style="color: #000000; font-weight: bold;">/</span>usr<span style="color: #000000; font-weight: bold;">/</span>lib64 <span style="color: #007800;">threading</span>=multi <span style="color: #660033;">--layout</span>=tagged <span style="color: #c20cb9; font-weight: bold;">install</span> <span style="color: #007800;">cxxflags</span>=-fPIC
    <span style="color: #666666; font-style: italic;">#编译静态库，不知道有没有用...</span>
    .<span style="color: #000000; font-weight: bold;">/</span>bjam <span style="color: #660033;">--layout</span>=tagged <span style="color: #660033;">--libdir</span>=<span style="color: #000000; font-weight: bold;">/</span>usr<span style="color: #000000; font-weight: bold;">/</span>lib64 <span style="color: #007800;">cxxflags</span>=-fPIC \
    <span style="color: #007800;">link</span>=static <span style="color: #007800;">threading</span>=multi runtime-link=static <span style="color: #c20cb9; font-weight: bold;">install</span></pre></td></tr></table><p class="theCode" style="display:none;">cd boost_1_46_1
    sh ./bootstrap.sh
    #注意要加上 cxxflags=-fPIC 参数，否则后面编译失败
    ./bjam --libdir=/usr/lib64 threading=multi --layout=tagged install cxxflags=-fPIC
    #编译静态库，不知道有没有用...
    ./bjam --layout=tagged --libdir=/usr/lib64 cxxflags=-fPIC \
    link=static threading=multi runtime-link=static install</p></div>
    ";i:3;s:390:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #c20cb9; font-weight: bold;">sh</span> .<span style="color: #000000; font-weight: bold;">/</span>buildall.sh -noclean -skiptests</pre></td></tr></table><p class="theCode" style="display:none;">sh ./buildall.sh -noclean -skiptests</p></div>
    ";i:4;s:739:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="other" style="font-family:monospace;">Linking CXX executable ../../build/debug/common/atomic-test
    /usr/bin/ld: cannot find -lboost_date_time
    collect2: ld returned 1 exit status
    make[2]: *** [be/build/debug/common/atomic-test] Error 1
    make[1]: *** [be/src/common/CMakeFiles/atomic-test.dir/all] Error 2</pre></td></tr></table><p class="theCode" style="display:none;">Linking CXX executable ../../build/debug/common/atomic-test
    /usr/bin/ld: cannot find -lboost_date_time
    collect2: ld returned 1 exit status
    make[2]: *** [be/build/debug/common/atomic-test] Error 1
    make[1]: *** [be/src/common/CMakeFiles/atomic-test.dir/all] Error 2</p></div>
    ";i:5;s:389:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="other" style="font-family:monospace;">find_package(Boost REQUIRED COMPONENTS thread regex-mt system-mt filesystem-mt date_time-mt)</pre></td></tr></table><p class="theCode" style="display:none;">find_package(Boost REQUIRED COMPONENTS thread regex-mt system-mt filesystem-mt date_time-mt)</p></div>
    ";i:6;s:523:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="other" style="font-family:monospace;">set(Boost_DEBUG FALSE)
    set(Boost_USE_STATIC_LIBS   ON)
    set(Boost_USE_STATIC_RUNTIME ON)
    set(Boost_USE_MULTITHREADED ON)
    add_definitions(-DBOOST_ALL_NO_LIB)</pre></td></tr></table><p class="theCode" style="display:none;">set(Boost_DEBUG FALSE)
    set(Boost_USE_STATIC_LIBS   ON)
    set(Boost_USE_STATIC_RUNTIME ON)
    set(Boost_USE_MULTITHREADED ON)
    add_definitions(-DBOOST_ALL_NO_LIB)</p></div>
    ";i:7;s:1175:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="other" style="font-family:monospace;">找到JAVA_AWT_LIBRARY_DIRECTORIES，增加路径（和你jdk位置相关）
    /usr/java/jdk1.7.0_67-cloudera/jre/lib/amd64/
    找到JAVA_AWT_INCLUDE_DIRECTORIES，增加路径
    /usr/java/jdk1.7.0_67-cloudera/include
    其他路径注释掉
    另外我还设定了几个路径
    set(JAVA_INCLUDE_PATH
     /usr/java/jdk1.7.0_67-cloudera/include
    )
    set(JAVA_INCLUDE_PATH2
     /usr/java/jdk1.7.0_67-cloudera/include/linux/
    )
    set(JAVA_AWT_INCLUDE_PATH
     /usr/java/jdk1.7.0_67-cloudera/include
    )</pre></td></tr></table><p class="theCode" style="display:none;">找到JAVA_AWT_LIBRARY_DIRECTORIES，增加路径（和你jdk位置相关）
    /usr/java/jdk1.7.0_67-cloudera/jre/lib/amd64/
    找到JAVA_AWT_INCLUDE_DIRECTORIES，增加路径
    /usr/java/jdk1.7.0_67-cloudera/include
    其他路径注释掉
    另外我还设定了几个路径
    set(JAVA_INCLUDE_PATH
     /usr/java/jdk1.7.0_67-cloudera/include
    )
    set(JAVA_INCLUDE_PATH2
     /usr/java/jdk1.7.0_67-cloudera/include/linux/
    )
    set(JAVA_AWT_INCLUDE_PATH
     /usr/java/jdk1.7.0_67-cloudera/include
    )</p></div>
    ";}
categories:
  - hadoop
tags:
  - impala

---
使用redhat5.8没编译成功，改用redhat6.4最终编译成功。
参考官方的文档https://github.com/cloudera/Impala/tree/v1.2.2
不知道官方的readme.md在新的版本为什么删掉了。。。囧
## 准备条件

安装必须要的包，jdk，llvm，maven
注意它要求用oracle的jdk，redhat默认是openjdk，可以参考这里安装 http://unix.stackexchange.com/questions/63587/how-to-install-g-4-7-2-c11-on-centos-5-x
&nbsp;
## 安装boost

CentOS 6.4上预装的是boost 1.41，但是impala需要更高版本的boost库（Note: Impala requires Boost 1.4.2 or later），所以先卸载掉boost 1.41
<pre lang="bash" escaped="true">rpm -e `rpm -qa|grep boost`</pre>
<pre lang="bash" escaped="true">cd boost_1_46_1
sh ./bootstrap.sh
#注意要加上 cxxflags=-fPIC 参数，否则后面编译失败
./bjam --libdir=/usr/lib64 threading=multi --layout=tagged install cxxflags=-fPIC
#编译静态库，不知道有没有用...
./bjam --layout=tagged --libdir=/usr/lib64 cxxflags=-fPIC \
link=static threading=multi runtime-link=static install</pre>
## 编译impala

把代码下载下来，由于不是直接从git下载来的，所以用git init初始化一次。另外注意里面有clean的选项，使用git来clean会导致一些代码被删掉。
<pre lang="bash" escaped="true">sh ./buildall.sh -noclean -skiptests</pre>
bulitall.sh实际会用到bin下面的脚本，可以都看一下
## 报错处理

<pre lang="other" escaped="true">Linking CXX executable ../../build/debug/common/atomic-test
/usr/bin/ld: cannot find -lboost_date_time
collect2: ld returned 1 exit status
make[2]: *** [be/build/debug/common/atomic-test] Error 1
make[1]: *** [be/src/common/CMakeFiles/atomic-test.dir/all] Error 2
</pre>
我们用的是mt（多线程）的库，所以要改一下  
修改了be/CMakeLists.txt的216行，将原有的：  
-lrt -lboost\_date\_time  
改为  
-lrt -lboost\_date\_time-mt  
如果要静态编译，要把-lboost\_date\_time去掉（这里我需要静态编译，所以把它去掉了）  
修改./CMakeLists.txt，加入date_time-mt
<pre lang="other" escaped="true">find_package(Boost REQUIRED COMPONENTS thread regex-mt system-mt filesystem-mt date_time-mt)</pre>
修改./CMakeLists.txt找到 Boost_DEBUG 这一行，加上着一些
<pre lang="other" escaped="true">set(Boost_DEBUG FALSE)
set(Boost_USE_STATIC_LIBS   ON)
set(Boost_USE_STATIC_RUNTIME ON)
set(Boost_USE_MULTITHREADED ON)
add_definitions(-DBOOST_ALL_NO_LIB)</pre>
编译后的文件在 be/bulid里面，编译出来的东西有200MB+，和官方的比20MB吓尿了好吧。  
执行strip &#8211;strip-debug impalad 会变成30MB+
### 报错Could NOT find JNI (missing: JNI\_INCLUDE\_DIRS)

修改cmake_modules/FindJNI.cmake文件
<pre lang="other" escaped="true">找到JAVA_AWT_LIBRARY_DIRECTORIES，增加路径（和你jdk位置相关）
/usr/java/jdk1.7.0_67-cloudera/jre/lib/amd64/
找到JAVA_AWT_INCLUDE_DIRECTORIES，增加路径
/usr/java/jdk1.7.0_67-cloudera/include
其他路径注释掉
另外我还设定了几个路径
set(JAVA_INCLUDE_PATH
 /usr/java/jdk1.7.0_67-cloudera/include
)
set(JAVA_INCLUDE_PATH2
 /usr/java/jdk1.7.0_67-cloudera/include/linux/
)
set(JAVA_AWT_INCLUDE_PATH
 /usr/java/jdk1.7.0_67-cloudera/include
)</pre>
&nbsp;
## cdh4.5 hive的bug

impala2.0.0通过yum方法安装中，会使用cdh4.5的lib  
cdh4.5中，org.apache.hadoop.hive.metastore.HiveMetaStoreClient有个bug，在每次连接metastore的时候都会等3秒钟，可以从catalog的日志看到，如果用background-load的方法会很慢。  
照着 cdh4.6的代码改就可以了。一个低级的错误http://www.grepcode.com/file/repository.cloudera.com/content/repositories/releases/org.apache.hive/hive-metastore/0.10.0-cdh4.6.0/org/apache/hadoop/hive/metastore/HiveMetaStoreClient.java#314  
把编译好的包替换掉，目录在/usr/lib/impala里
## 参考

https://github.com/cloudera/Impala/tree/v1.2.2  
http://blog.csdn.net/vah101/article/details/32343471  
http://blog.chinaunix.net/uid-21519621-id-3952587.html  
编译release版本 http://johnjianfang.blogspot.com/2013/06/build-impala-release.html