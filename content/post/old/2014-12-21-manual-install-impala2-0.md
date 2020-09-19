---
title: 在Redhat6.4手动安装impala2.0
author: fatkun
type: post
date: 2014-12-21T08:21:17+00:00
url: /2014/12/manual-install-impala2-0.html
duoshuo_thread_id:
  - 6300410881171800833
wp-syntax-cache-content:
  - |
    a:13:{i:1;s:570:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #c20cb9; font-weight: bold;">wget</span> <span style="color: #660033;">-r</span> <span style="color: #660033;">-np</span> <span style="color: #660033;">-k</span> <span style="color: #ff0000;">'http://archive.cloudera.com/impala/redhat/6/x86_64/impala/2.0.0/'</span></pre></td></tr></table><p class="theCode" style="display:none;">wget -r -np -k 'http://archive.cloudera.com/impala/redhat/6/x86_64/impala/2.0.0/'</p></div>
    ";i:2;s:1019:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="xml" style="font-family:monospace;">server  {
                    listen       9500;
                    server_name www.lnmp.org;
                    index index.html index.htm index.php;
                    root  /home/kpi/impala/archive.cloudera.com;
                    autoindex on;              #打开索引功能
                    autoindex_exact_size off;  #人性化方式显示大小
                    autoindex_localtime on;    #显示服务器时间
    }</pre></td></tr></table><p class="theCode" style="display:none;">server  {
                    listen       9500;
                    server_name www.lnmp.org;
                    index index.html index.htm index.php;
                    root  /home/kpi/impala/archive.cloudera.com;
                    autoindex on;              #打开索引功能
                    autoindex_exact_size off;  #人性化方式显示大小
                    autoindex_localtime on;    #显示服务器时间
    }</p></div>
    ";i:3;s:621:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="xml" style="font-family:monospace;">[cloudera-impala]
    name=Impala
    baseurl=http://archive.cloudera.com/impala/redhat/6/x86_64/impala/2.0.0/
    gpgkey = http://archive.cloudera.com/impala/redhat/6/x86_64/impala/RPM-GPG-KEY-cloudera    
    gpgcheck = 1</pre></td></tr></table><p class="theCode" style="display:none;">[cloudera-impala]
    name=Impala
    baseurl=http://archive.cloudera.com/impala/redhat/6/x86_64/impala/2.0.0/
    gpgkey = http://archive.cloudera.com/impala/redhat/6/x86_64/impala/RPM-GPG-KEY-cloudera    
    gpgcheck = 1</p></div>
    ";i:4;s:350:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #c20cb9; font-weight: bold;">yum install</span> impala impala-server impala-shell</pre></td></tr></table><p class="theCode" style="display:none;">yum install impala impala-server impala-shell</p></div>
    ";i:5;s:350:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #c20cb9; font-weight: bold;">yum install</span> impala-state-store impala-catalog</pre></td></tr></table><p class="theCode" style="display:none;">yum install impala-state-store impala-catalog</p></div>
    ";i:6;s:2756:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #c20cb9; font-weight: bold;">ln</span> <span style="color: #660033;">-s</span> <span style="color: #000000; font-weight: bold;">/</span>etc<span style="color: #000000; font-weight: bold;">/</span>hive<span style="color: #000000; font-weight: bold;">/</span>conf<span style="color: #000000; font-weight: bold;">/</span>hive-site.xml <span style="color: #000000; font-weight: bold;">/</span>etc<span style="color: #000000; font-weight: bold;">/</span>impala<span style="color: #000000; font-weight: bold;">/</span>conf<span style="color: #000000; font-weight: bold;">/</span>
    <span style="color: #c20cb9; font-weight: bold;">ln</span> <span style="color: #660033;">-s</span> <span style="color: #000000; font-weight: bold;">/</span>etc<span style="color: #000000; font-weight: bold;">/</span>hive<span style="color: #000000; font-weight: bold;">/</span>conf<span style="color: #000000; font-weight: bold;">/</span>hive-env.sh <span style="color: #000000; font-weight: bold;">/</span>etc<span style="color: #000000; font-weight: bold;">/</span>impala<span style="color: #000000; font-weight: bold;">/</span>conf<span style="color: #000000; font-weight: bold;">/</span>
    <span style="color: #c20cb9; font-weight: bold;">ln</span> <span style="color: #660033;">-s</span> <span style="color: #000000; font-weight: bold;">/</span>etc<span style="color: #000000; font-weight: bold;">/</span>hadoop<span style="color: #000000; font-weight: bold;">/</span>conf<span style="color: #000000; font-weight: bold;">/</span>core-site.xml <span style="color: #000000; font-weight: bold;">/</span>etc<span style="color: #000000; font-weight: bold;">/</span>impala<span style="color: #000000; font-weight: bold;">/</span>conf<span style="color: #000000; font-weight: bold;">/</span>
    <span style="color: #c20cb9; font-weight: bold;">cp</span> <span style="color: #000000; font-weight: bold;">/</span>etc<span style="color: #000000; font-weight: bold;">/</span>hadoop<span style="color: #000000; font-weight: bold;">/</span>conf<span style="color: #000000; font-weight: bold;">/</span>hdfs-site.xml <span style="color: #000000; font-weight: bold;">/</span>etc<span style="color: #000000; font-weight: bold;">/</span>impala<span style="color: #000000; font-weight: bold;">/</span>conf<span style="color: #000000; font-weight: bold;">/</span></pre></td></tr></table><p class="theCode" style="display:none;">ln -s /etc/hive/conf/hive-site.xml /etc/impala/conf/
    ln -s /etc/hive/conf/hive-env.sh /etc/impala/conf/
    ln -s /etc/hadoop/conf/core-site.xml /etc/impala/conf/
    cp /etc/hadoop/conf/hdfs-site.xml /etc/impala/conf/</p></div>
    ";i:7;s:1378:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="xml" style="font-family:monospace;"><span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;property<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;name<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>dfs.client.file-block-storage-locations.timeout<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/name<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;value<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>3000<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/value<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/property<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre></td></tr></table><p class="theCode" style="display:none;">&lt;property&gt;
    &lt;name&gt;dfs.client.file-block-storage-locations.timeout&lt;/name&gt;
    &lt;value&gt;3000&lt;/value&gt;
    &lt;/property&gt;</p></div>
    ";i:8;s:1060:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #c20cb9; font-weight: bold;">mkdir</span> <span style="color: #660033;">-p</span> <span style="color: #000000; font-weight: bold;">/</span>home<span style="color: #000000; font-weight: bold;">/</span>hadoop<span style="color: #000000; font-weight: bold;">/</span>log<span style="color: #000000; font-weight: bold;">/</span>impala<span style="color: #000000; font-weight: bold;">/</span>
    <span style="color: #c20cb9; font-weight: bold;">chown</span> kpi:kpi <span style="color: #000000; font-weight: bold;">/</span>home<span style="color: #000000; font-weight: bold;">/</span>hadoop<span style="color: #000000; font-weight: bold;">/</span>log<span style="color: #000000; font-weight: bold;">/</span>impala<span style="color: #000000; font-weight: bold;">/</span></pre></td></tr></table><p class="theCode" style="display:none;">mkdir -p /home/hadoop/log/impala/
    chown kpi:kpi /home/hadoop/log/impala/</p></div>
    ";i:9;s:4620:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #007800;">IMPALA_CATALOG_SERVICE_HOST</span>=catalog的机器名或IP
    <span style="color: #007800;">IMPALA_STATE_STORE_HOST</span>=statestore的机器名或IP
    <span style="color: #007800;">IMPALA_STATE_STORE_PORT</span>=<span style="color: #000000;">24000</span>
    <span style="color: #007800;">IMPALA_BACKEND_PORT</span>=<span style="color: #000000;">22000</span>
    <span style="color: #007800;">IMPALA_LOG_DIR</span>=<span style="color: #000000; font-weight: bold;">/</span>home<span style="color: #000000; font-weight: bold;">/</span>hadoop<span style="color: #000000; font-weight: bold;">/</span>log<span style="color: #000000; font-weight: bold;">/</span>impala
    &nbsp;
    <span style="color: #007800;">IMPALA_CATALOG_ARGS</span>=<span style="color: #ff0000;">&quot; -log_dir=<span style="color: #007800;">${IMPALA_LOG_DIR}</span> &quot;</span>
    <span style="color: #007800;">IMPALA_STATE_STORE_ARGS</span>=<span style="color: #ff0000;">&quot; -log_dir=<span style="color: #007800;">${IMPALA_LOG_DIR}</span> -state_store_port=<span style="color: #007800;">${IMPALA_STATE_STORE_PORT}</span>&quot;</span>
    <span style="color: #007800;">IMPALA_SERVER_ARGS</span>=<span style="color: #ff0000;">&quot; <span style="color: #000099; font-weight: bold;">\
    </span>-mem_limit=4294967296 <span style="color: #000099; font-weight: bold;">\
    </span>-enable_webserver=true <span style="color: #000099; font-weight: bold;">\
    </span>-webserver_port=25000 <span style="color: #000099; font-weight: bold;">\
    </span>-beeswax_port=21000 <span style="color: #000099; font-weight: bold;">\
    </span>-hs2_port=21050 <span style="color: #000099; font-weight: bold;">\
    </span>    -log_dir=<span style="color: #007800;">${IMPALA_LOG_DIR}</span> <span style="color: #000099; font-weight: bold;">\
    </span>    -catalog_service_host=<span style="color: #007800;">${IMPALA_CATALOG_SERVICE_HOST}</span> <span style="color: #000099; font-weight: bold;">\
    </span>    -state_store_port=<span style="color: #007800;">${IMPALA_STATE_STORE_PORT}</span> <span style="color: #000099; font-weight: bold;">\
    </span>    -use_statestore <span style="color: #000099; font-weight: bold;">\
    </span>    -state_store_host=<span style="color: #007800;">${IMPALA_STATE_STORE_HOST}</span> <span style="color: #000099; font-weight: bold;">\
    </span>    -be_port=<span style="color: #007800;">${IMPALA_BACKEND_PORT}</span>&quot;</span>
    &nbsp;
    <span style="color: #007800;">ENABLE_CORE_DUMPS</span>=<span style="color: #c20cb9; font-weight: bold;">false</span>
    &nbsp;
    <span style="color: #666666; font-style: italic;"># LIBHDFS_OPTS=-Djava.library.path=/usr/lib/impala/lib</span>
    <span style="color: #666666; font-style: italic;"># MYSQL_CONNECTOR_JAR=/usr/share/java/mysql-connector-java.jar</span>
    <span style="color: #666666; font-style: italic;"># IMPALA_BIN=/usr/lib/impala/sbin</span>
    <span style="color: #666666; font-style: italic;"># IMPALA_HOME=/usr/lib/impala</span>
    <span style="color: #666666; font-style: italic;"># HIVE_HOME=/usr/lib/hive</span>
    <span style="color: #666666; font-style: italic;"># HBASE_HOME=/usr/lib/hbase</span>
    <span style="color: #666666; font-style: italic;"># IMPALA_CONF_DIR=/etc/impala/conf</span>
    <span style="color: #666666; font-style: italic;"># HADOOP_CONF_DIR=/etc/hadoop/conf</span></pre></td></tr></table><p class="theCode" style="display:none;">IMPALA_CATALOG_SERVICE_HOST=catalog的机器名或IP
    IMPALA_STATE_STORE_HOST=statestore的机器名或IP
    IMPALA_STATE_STORE_PORT=24000
    IMPALA_BACKEND_PORT=22000
    IMPALA_LOG_DIR=/home/hadoop/log/impala
    
    IMPALA_CATALOG_ARGS=&quot; -log_dir=${IMPALA_LOG_DIR} &quot;
    IMPALA_STATE_STORE_ARGS=&quot; -log_dir=${IMPALA_LOG_DIR} -state_store_port=${IMPALA_STATE_STORE_PORT}&quot;
    IMPALA_SERVER_ARGS=&quot; \
    -mem_limit=4294967296 \
    -enable_webserver=true \
    -webserver_port=25000 \
    -beeswax_port=21000 \
    -hs2_port=21050 \
        -log_dir=${IMPALA_LOG_DIR} \
        -catalog_service_host=${IMPALA_CATALOG_SERVICE_HOST} \
        -state_store_port=${IMPALA_STATE_STORE_PORT} \
        -use_statestore \
        -state_store_host=${IMPALA_STATE_STORE_HOST} \
        -be_port=${IMPALA_BACKEND_PORT}&quot;
    
    ENABLE_CORE_DUMPS=false
    
    # LIBHDFS_OPTS=-Djava.library.path=/usr/lib/impala/lib
    # MYSQL_CONNECTOR_JAR=/usr/share/java/mysql-connector-java.jar
    # IMPALA_BIN=/usr/lib/impala/sbin
    # IMPALA_HOME=/usr/lib/impala
    # HIVE_HOME=/usr/lib/hive
    # HBASE_HOME=/usr/lib/hbase
    # IMPALA_CONF_DIR=/etc/impala/conf
    # HADOOP_CONF_DIR=/etc/hadoop/conf</p></div>
    ";i:10;s:384:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;">service impala-state-store start
    service impala-catalog start
    service impala-server start</pre></td></tr></table><p class="theCode" style="display:none;">service impala-state-store start
    service impala-catalog start
    service impala-server start</p></div>
    ";i:11;s:619:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #c20cb9; font-weight: bold;">ps</span> auxf<span style="color: #000000; font-weight: bold;">|</span><span style="color: #c20cb9; font-weight: bold;">grep</span> state
    <span style="color: #c20cb9; font-weight: bold;">ps</span> auxf<span style="color: #000000; font-weight: bold;">|</span><span style="color: #c20cb9; font-weight: bold;">grep</span> catalog</pre></td></tr></table><p class="theCode" style="display:none;">ps auxf|grep state
    ps auxf|grep catalog</p></div>
    ";i:12;s:858:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="xml" style="font-family:monospace;">[cloudera-gplextras5]
    # Packages for Cloudera's GPLExtras, Version 5, on RedHat or CentOS 6 x86_64
    name=Cloudera's GPLExtras, Version 5
    baseurl=http://archive.cloudera.com/gplextras/redhat/6/x86_64/gplextras/4.3.0/
    gpgkey = http://archive.cloudera.com/gplextras/redhat/6/x86_64/gplextras/RPM-GPG-KEY-cloudera    
    gpgcheck = 1</pre></td></tr></table><p class="theCode" style="display:none;">[cloudera-gplextras5]
    # Packages for Cloudera's GPLExtras, Version 5, on RedHat or CentOS 6 x86_64
    name=Cloudera's GPLExtras, Version 5
    baseurl=http://archive.cloudera.com/gplextras/redhat/6/x86_64/gplextras/4.3.0/
    gpgkey = http://archive.cloudera.com/gplextras/redhat/6/x86_64/gplextras/RPM-GPG-KEY-cloudera    
    gpgcheck = 1</p></div>
    ";i:13;s:316:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #c20cb9; font-weight: bold;">yum install</span> impala-lzo-2.0.0</pre></td></tr></table><p class="theCode" style="display:none;">yum install impala-lzo-2.0.0</p></div>
    ";}
categories:
  - hadoop
tags:
  - 2.0.0
  - impala

---
##  背景

已经通过cloudera manager装好了hadoop，但由于不敢升级cm，所以单独升级impala，采用yum的安装方式。原本已经安装了impala1.1，现在升级到impala2.0。所以有些配置没有说明，请参考官方文档。
## 在本地做个镜像

把需要用到的rpm下载下来
<pre lang="bash" escaped="true">wget -r -np -k 'http://archive.cloudera.com/impala/redhat/6/x86_64/impala/2.0.0/'</pre>
&nbsp;
配置一个nginx，用来提供下载
nginx配置
<pre lang="xml" escaped="true">server  {
                listen       9500;
                server_name www.lnmp.org;
                index index.html index.htm index.php;
                root  /home/kpi/impala/archive.cloudera.com;
                autoindex on;              #打开索引功能
                autoindex_exact_size off;  #人性化方式显示大小
                autoindex_localtime on;    #显示服务器时间
}

</pre>
## 配置repo

把以下内容保存为文件 impala.repo 到 /etc/yum.repos.d/目录下， 下面的地址 archive.cloudera.com 可以换成你本地镜像的地址
<pre lang="xml">[cloudera-impala]
name=Impala
baseurl=http://archive.cloudera.com/impala/redhat/6/x86_64/impala/2.0.0/
gpgkey = http://archive.cloudera.com/impala/redhat/6/x86_64/impala/RPM-GPG-KEY-cloudera    
gpgcheck = 1
</pre>
&nbsp;
## 安装

安装服务，所有机器安装
<pre lang="bash" escaped="true">yum install impala impala-server impala-shell</pre>
在某台机器上装state-store这些启动脚本
<pre lang="bash" escaped="true">yum install impala-state-store impala-catalog</pre>
## 配置

<pre lang="bash" escaped="true">ln -s /etc/hive/conf/hive-site.xml /etc/impala/conf/
ln -s /etc/hive/conf/hive-env.sh /etc/impala/conf/
ln -s /etc/hadoop/conf/core-site.xml /etc/impala/conf/
cp /etc/hadoop/conf/hdfs-site.xml /etc/impala/conf/
</pre>
hdfs-site.xml配置不能直接用客户端的配置，会缺少某个配置导致impala-server启动不了。如果启动不了可以检查impala的日志。
在hdfs-site.xml加入
<pre lang="xml" escaped="true">&lt;property&gt;
&lt;name&gt;dfs.client.file-block-storage-locations.timeout&lt;/name&gt;
&lt;value&gt;3000&lt;/value&gt;
&lt;/property&gt;</pre>
hdfs配置查看下面的网址，注意影响性能的Short-Circuit Reads选项  
http://www.cloudera.com/content/cloudera/en/documentation/core/latest/topics/impala\_config\_performance.html?scroll=config_performance
### 修改impala默认用户为kpi

这个只是我们需要用kpi这个账号来读取数据，如果你使用默认用户impala也是可以的，注意要在hdfs配置这个用户可以直接读取hdfs
修改/etc/init.d/impala-server, /etc/init.d/impala-state-store,/etc/init.d/impala-catalog 文件，  
找到 SVC\_USER=&#8221;impala&#8221; 改为 SVC\_USER=&#8221;kpi&#8221;  
找到install -d -m 0755 -o impala -g impala /var/run/impala 改为 install -d -m 0755 -o kpi -g kpi /var/run/impala  
创建日志目录
<pre lang="bash" escaped="true">mkdir -p /home/hadoop/log/impala/
chown kpi:kpi /home/hadoop/log/impala/</pre>
修改impala 的默认配置/etc/default/impala文件
<pre lang="bash" escaped="true">IMPALA_CATALOG_SERVICE_HOST=catalog的机器名或IP
IMPALA_STATE_STORE_HOST=statestore的机器名或IP
IMPALA_STATE_STORE_PORT=24000
IMPALA_BACKEND_PORT=22000
IMPALA_LOG_DIR=/home/hadoop/log/impala

IMPALA_CATALOG_ARGS=" -log_dir=${IMPALA_LOG_DIR} "
IMPALA_STATE_STORE_ARGS=" -log_dir=${IMPALA_LOG_DIR} -state_store_port=${IMPALA_STATE_STORE_PORT}"
IMPALA_SERVER_ARGS=" \
-mem_limit=4294967296 \
-enable_webserver=true \
-webserver_port=25000 \
-beeswax_port=21000 \
-hs2_port=21050 \
    -log_dir=${IMPALA_LOG_DIR} \
    -catalog_service_host=${IMPALA_CATALOG_SERVICE_HOST} \
    -state_store_port=${IMPALA_STATE_STORE_PORT} \
    -use_statestore \
    -state_store_host=${IMPALA_STATE_STORE_HOST} \
    -be_port=${IMPALA_BACKEND_PORT}"

ENABLE_CORE_DUMPS=false

# LIBHDFS_OPTS=-Djava.library.path=/usr/lib/impala/lib
# MYSQL_CONNECTOR_JAR=/usr/share/java/mysql-connector-java.jar
# IMPALA_BIN=/usr/lib/impala/sbin
# IMPALA_HOME=/usr/lib/impala
# HIVE_HOME=/usr/lib/hive
# HBASE_HOME=/usr/lib/hbase
# IMPALA_CONF_DIR=/etc/impala/conf
# HADOOP_CONF_DIR=/etc/hadoop/conf</pre>
&nbsp;
## 启动

<pre lang="bash" escaped="true">service impala-state-store start
service impala-catalog start
service impala-server start</pre>
报错/etc/init.d/impala-state-store: line 35: /etc/default/hadoop: No such file or directory 这个无关紧要，找不到hadoop默认配置文件
&nbsp;
## 报错处理

在redhat5.x版本中启动impala-shell会报sasl的错误，需要用pip安装python26-libs ,sasl
报错 ERROR: block location tracking is not properly enabled because  
&#8211; dfs.client.file-block-storage-locations.timeout is too low. It should be at least 3000.
是因为hdfs的配置不对，需要在hdfs_site.xml加入dfs.client.file-block-storage-locations.timeout配置,见上面的配置
## 检查进程

看一下进程是否都已经起来了
<pre lang="bash" escaped="true">ps auxf|grep state
ps auxf|grep catalog
</pre>
## 安装impala lzo（可选）

加入cloudera-gplextras5.repo
<pre lang="xml" escaped="true">[cloudera-gplextras5]
# Packages for Cloudera's GPLExtras, Version 5, on RedHat or CentOS 6 x86_64
name=Cloudera's GPLExtras, Version 5
baseurl=http://archive.cloudera.com/gplextras/redhat/6/x86_64/gplextras/4.3.0/
gpgkey = http://archive.cloudera.com/gplextras/redhat/6/x86_64/gplextras/RPM-GPG-KEY-cloudera    
gpgcheck = 1</pre>
安装
<pre lang="bash" escaped="true">yum install impala-lzo-2.0.0</pre>
&nbsp;
## 参考

<http://blog.javachen.com/2013/03/29/install-impala/>  
[http://www.cloudera.com/content/cloudera/en/documentation/core/latest/topics/impala\_noncm\_installation.html][1]

 [1]: http://www.cloudera.com/content/cloudera/en/documentation/core/latest/topics/impala_noncm_installation.html