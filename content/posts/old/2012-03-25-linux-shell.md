---
title: 记录一些常用的linux shell命令
author: fatkun
type: post
date: 2012-03-25T13:31:35+00:00
url: /2012/03/linux-shell.html
duoshuo_thread_id:
  - 6300408840718385921
wp-syntax-cache-content:
  - |
    a:22:{i:1;s:451:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #666666; font-style: italic;"># 从第0位开始截取2个字符</span>
    <span style="color: #7a0874; font-weight: bold;">echo</span> <span style="color: #800000;">${a:0:2}</span></pre></td></tr></table><p class="theCode" style="display:none;"># 从第0位开始截取2个字符
    echo ${a:0:2}</p></div>
    ";i:2;s:1496:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">if</span> <span style="color: #7a0874; font-weight: bold;">&#91;</span> <span style="color: #ff0000;">&quot;<span style="color: #007800;">$name</span>&quot;</span> == <span style="color: #ff0000;">&quot;Fatkun&quot;</span> <span style="color: #7a0874; font-weight: bold;">&#93;</span>; <span style="color: #000000; font-weight: bold;">then</span>
        <span style="color: #7a0874; font-weight: bold;">echo</span> <span style="color: #ff0000;">&quot;Hi!Fatkun&quot;</span>
    <span style="color: #000000; font-weight: bold;">elif</span> <span style="color: #7a0874; font-weight: bold;">&#91;</span> ... <span style="color: #7a0874; font-weight: bold;">&#93;</span>; <span style="color: #000000; font-weight: bold;">then</span>
        <span style="color: #7a0874; font-weight: bold;">echo</span> <span style="color: #ff0000;">&quot;...&quot;</span>
    <span style="color: #000000; font-weight: bold;">else</span>
        <span style="color: #7a0874; font-weight: bold;">echo</span> <span style="color: #ff0000;">&quot;...&quot;</span>
    <span style="color: #000000; font-weight: bold;">fi</span></pre></td></tr></table><p class="theCode" style="display:none;">if [ &quot;$name&quot; == &quot;Fatkun&quot; ]; then
        echo &quot;Hi!Fatkun&quot;
    elif [ ... ]; then
        echo &quot;...&quot;
    else
        echo &quot;...&quot;
    fi</p></div>
    ";i:3;s:2720:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">case</span>  $變數名稱 <span style="color: #000000; font-weight: bold;">in</span>   <span style="color: #000000; font-weight: bold;">&lt;</span>==關鍵字為 <span style="color: #000000; font-weight: bold;">case</span> ，還有變數前有錢字號
      <span style="color: #ff0000;">&quot;第一個變數內容&quot;</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>   <span style="color: #000000; font-weight: bold;">&lt;</span>==每個變數內容建議用雙引號括起來，關鍵字則為小括號 <span style="color: #7a0874; font-weight: bold;">&#41;</span>
        程式段
        <span style="color: #000000; font-weight: bold;">;;</span>            <span style="color: #000000; font-weight: bold;">&lt;</span>==每個類別結尾使用兩個連續的分號來處理！
      <span style="color: #ff0000;">&quot;第二個變數內容&quot;</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
        程式段
        <span style="color: #000000; font-weight: bold;">;;</span>
      <span style="color: #000000; font-weight: bold;">*</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>                  <span style="color: #000000; font-weight: bold;">&lt;</span>==最後一個變數內容都會用 <span style="color: #000000; font-weight: bold;">*</span> 來代表所有其他值
        不包含第一個變數內容與第二個變數內容的其他程式執行段
        <span style="color: #7a0874; font-weight: bold;">exit</span> <span style="color: #000000;">1</span>
        <span style="color: #000000; font-weight: bold;">;;</span>
    <span style="color: #000000; font-weight: bold;">esac</span>                  <span style="color: #000000; font-weight: bold;">&lt;</span>==最終的 <span style="color: #000000; font-weight: bold;">case</span> 結尾！『反過來寫』思考一下！</pre></td></tr></table><p class="theCode" style="display:none;">case  $變數名稱 in   &lt;==關鍵字為 case ，還有變數前有錢字號
      &quot;第一個變數內容&quot;)   &lt;==每個變數內容建議用雙引號括起來，關鍵字則為小括號 )
        程式段
        ;;            &lt;==每個類別結尾使用兩個連續的分號來處理！
      &quot;第二個變數內容&quot;)
        程式段
        ;;
      *)                  &lt;==最後一個變數內容都會用 * 來代表所有其他值
        不包含第一個變數內容與第二個變數內容的其他程式執行段
        exit 1
        ;;
    esac                  &lt;==最終的 case 結尾！『反過來寫』思考一下！</p></div>
    ";i:4;s:1113:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">while</span> <span style="color: #7a0874; font-weight: bold;">&#91;</span> condition <span style="color: #7a0874; font-weight: bold;">&#93;</span>  <span style="color: #000000; font-weight: bold;">&lt;</span>==中括號內的狀態就是判斷式
    <span style="color: #000000; font-weight: bold;">do</span>            <span style="color: #000000; font-weight: bold;">&lt;</span>==<span style="color: #000000; font-weight: bold;">do</span> 是迴圈的開始！
        程式段落
    <span style="color: #000000; font-weight: bold;">done</span>          <span style="color: #000000; font-weight: bold;">&lt;</span>==<span style="color: #000000; font-weight: bold;">done</span> 是迴圈的結束</pre></td></tr></table><p class="theCode" style="display:none;">while [ condition ]  &lt;==中括號內的狀態就是判斷式
    do            &lt;==do 是迴圈的開始！
        程式段落
    done          &lt;==done 是迴圈的結束</p></div>
    ";i:5;s:533:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">for</span> var <span style="color: #000000; font-weight: bold;">in</span> con1 con2 con3 ...
    <span style="color: #000000; font-weight: bold;">do</span>
        程式段
    <span style="color: #000000; font-weight: bold;">done</span></pre></td></tr></table><p class="theCode" style="display:none;">for var in con1 con2 con3 ...
    do
        程式段
    done</p></div>
    ";i:6;s:877:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #007800;">CLUSTERS</span>=<span style="color: #7a0874; font-weight: bold;">&#40;</span>aaa bbb ccc<span style="color: #7a0874; font-weight: bold;">&#41;</span>
    <span style="color: #000000; font-weight: bold;">for</span> cluster <span style="color: #000000; font-weight: bold;">in</span> <span style="color: #800000;">${CLUSTERS[@]}</span>;
    <span style="color: #000000; font-weight: bold;">do</span>
        <span style="color: #7a0874; font-weight: bold;">echo</span> <span style="color: #007800;">$cluster</span>
    <span style="color: #000000; font-weight: bold;">done</span></pre></td></tr></table><p class="theCode" style="display:none;">CLUSTERS=(aaa bbb ccc)
    for cluster in ${CLUSTERS[@]};
    do
        echo $cluster
    done</p></div>
    ";i:7;s:952:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">for</span><span style="color: #7a0874; font-weight: bold;">&#40;</span><span style="color: #7a0874; font-weight: bold;">&#40;</span><span style="color: #007800;">i</span>=<span style="color: #000000;">1</span>;i<span style="color: #000000; font-weight: bold;">&lt;</span><span style="color: #000000;">100</span>;i++<span style="color: #7a0874; font-weight: bold;">&#41;</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>;<span style="color: #000000; font-weight: bold;">do</span>
    <span style="color: #7a0874; font-weight: bold;">echo</span> <span style="color: #007800;">$i</span>
    <span style="color: #000000; font-weight: bold;">done</span></pre></td></tr></table><p class="theCode" style="display:none;">for((i=1;i&lt;100;i++));do
    echo $i
    done</p></div>
    ";i:8;s:2636:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #c20cb9; font-weight: bold;">sed</span> <span style="color: #660033;">-i</span> <span style="color: #ff0000;">&quot;s/oldstring/newstring/g&quot;</span> <span style="color: #c20cb9; font-weight: bold;">file</span> <span style="color: #666666; font-style: italic;">#在原文件修改</span>
    <span style="color: #c20cb9; font-weight: bold;">sed</span> <span style="color: #ff0000;">&quot;s/oldstring/newstring/g&quot;</span> <span style="color: #c20cb9; font-weight: bold;">file</span> <span style="color: #000000; font-weight: bold;">&gt;</span>file.new <span style="color: #666666; font-style: italic;"># 输出到其他文件</span>
    <span style="color: #007800;">file</span>=<span style="color: #ff0000;">&quot;/tmp/crontab_<span style="color: #780078;">`date +&quot;%H%M%S&quot;`</span>.bak&quot;</span>; crontab <span style="color: #660033;">-l</span> <span style="color: #000000; font-weight: bold;">&gt;</span> <span style="color: #007800;">$file</span>; <span style="color: #c20cb9; font-weight: bold;">sed</span> <span style="color: #ff0000;">&quot;s/\*\/5 \* \* \* \* run-parts/\* \* \* \* \* run-parts/g&quot;</span> <span style="color: #007800;">$file</span> <span style="color: #000000; font-weight: bold;">&gt;</span> <span style="color: #ff0000;">&quot;<span style="color: #007800;">$file</span>.new&quot;</span>; crontab <span style="color: #ff0000;">&quot;<span style="color: #007800;">$file</span>.new&quot;</span>; <span style="color: #666666; font-style: italic;"># 替换crontab文件</span>
    <span style="color: #c20cb9; font-weight: bold;">sed</span> <span style="color: #660033;">-r</span> <span style="color: #ff0000;">'s/^\s+([0-9]+) /\1|/g'</span>
    <span style="color: #c20cb9; font-weight: bold;">sed</span> <span style="color: #660033;">-i</span> <span style="color: #ff0000;">'$i\eeeeeeeee'</span>  urfile <span style="color: #666666; font-style: italic;"># 在倒数一行插入内容</span></pre></td></tr></table><p class="theCode" style="display:none;">sed -i &quot;s/oldstring/newstring/g&quot; file #在原文件修改
    sed &quot;s/oldstring/newstring/g&quot; file &gt;file.new # 输出到其他文件
    file=&quot;/tmp/crontab_`date +&quot;%H%M%S&quot;`.bak&quot;; crontab -l &gt; $file; sed &quot;s/\*\/5 \* \* \* \* run-parts/\* \* \* \* \* run-parts/g&quot; $file &gt; &quot;$file.new&quot;; crontab &quot;$file.new&quot;; # 替换crontab文件
    sed -r 's/^\s+([0-9]+) /\1|/g'
    sed -i '$i\eeeeeeeee'  urfile # 在倒数一行插入内容</p></div>
    ";i:9;s:1237:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #c20cb9; font-weight: bold;">tar</span> <span style="color: #660033;">--exclude</span>=log <span style="color: #660033;">-cvzf</span> xxx_<span style="color: #000000; font-weight: bold;">`</span><span style="color: #c20cb9; font-weight: bold;">date</span> +<span style="color: #ff0000;">&quot;%Y-%m-%d_%H_%M&quot;</span><span style="color: #000000; font-weight: bold;">`</span>.tar.gz .<span style="color: #000000; font-weight: bold;">/</span>xxx
    <span style="color: #666666; font-style: italic;"># 使用xz压缩，如果使用lzma压缩也是用XZ_OPT</span>
    <span style="color: #007800;">XZ_OPT</span>=-<span style="color: #000000;">1</span> <span style="color: #c20cb9; font-weight: bold;">tar</span> <span style="color: #660033;">-cf</span> <span style="color: #000000;">1</span>.tar.xz <span style="color: #660033;">--xz</span> xx.log</pre></td></tr></table><p class="theCode" style="display:none;">tar --exclude=log -cvzf xxx_`date +&quot;%Y-%m-%d_%H_%M&quot;`.tar.gz ./xxx
    # 使用xz压缩，如果使用lzma压缩也是用XZ_OPT
    XZ_OPT=-1 tar -cf 1.tar.xz --xz xx.log</p></div>
    ";i:10;s:1354:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">/</span>sbin<span style="color: #000000; font-weight: bold;">/</span><span style="color: #c20cb9; font-weight: bold;">ifconfig</span> <span style="color: #660033;">-a</span><span style="color: #000000; font-weight: bold;">|</span><span style="color: #c20cb9; font-weight: bold;">grep</span> inet<span style="color: #000000; font-weight: bold;">|</span><span style="color: #c20cb9; font-weight: bold;">grep</span> <span style="color: #660033;">-v</span> 127.0.0.1<span style="color: #000000; font-weight: bold;">|</span><span style="color: #c20cb9; font-weight: bold;">grep</span> <span style="color: #660033;">-v</span> inet6<span style="color: #000000; font-weight: bold;">|</span><span style="color: #c20cb9; font-weight: bold;">awk</span> <span style="color: #ff0000;">'{print $2}'</span><span style="color: #000000; font-weight: bold;">|</span><span style="color: #c20cb9; font-weight: bold;">tr</span> <span style="color: #660033;">-d</span> <span style="color: #ff0000;">&quot;addr:&quot;</span></pre></td></tr></table><p class="theCode" style="display:none;">/sbin/ifconfig -a|grep inet|grep -v 127.0.0.1|grep -v inet6|awk '{print $2}'|tr -d &quot;addr:&quot;</p></div>
    ";i:11;s:374:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="html" style="font-family:monospace;">grep -n -B1 -A1 &quot;关键字&quot; file  #匹配关键字的前一行与后一行.</pre></td></tr></table><p class="theCode" style="display:none;">grep -n -B1 -A1 &quot;关键字&quot; file  #匹配关键字的前一行与后一行.</p></div>
    ";i:12;s:1102:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #666666; font-style: italic;"># -e 参数指定用ssh传输</span>
    rsync <span style="color: #660033;">--exclude</span> <span style="color: #ff0000;">'logs'</span> <span style="color: #660033;">--size-only</span> <span style="color: #660033;">--progress</span> <span style="color: #660033;">-rave</span> <span style="color: #ff0000;">&quot;ssh -p2222&quot;</span> <span style="color: #000000; font-weight: bold;">/</span>home<span style="color: #000000; font-weight: bold;">/</span>xx<span style="color: #000000; font-weight: bold;">/</span> 用户名<span style="color: #000000; font-weight: bold;">@</span>IP地址:<span style="color: #000000; font-weight: bold;">/</span>tmp<span style="color: #000000; font-weight: bold;">/</span>xx</pre></td></tr></table><p class="theCode" style="display:none;"># -e 参数指定用ssh传输
    rsync --exclude 'logs' --size-only --progress -rave &quot;ssh -p2222&quot; /home/xx/ 用户名@IP地址:/tmp/xx</p></div>
    ";i:13;s:999:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #c20cb9; font-weight: bold;">gawk</span> <span style="color: #660033;">-F</span><span style="color: #ff0000;">'|'</span> <span style="color: #ff0000;">'BEGIN {OFS=&quot;|&quot;}{print $1,$2,$3}'</span>
    <span style="color: #c20cb9; font-weight: bold;">gawk</span> <span style="color: #ff0000;">'{a=index($0, &quot; from &quot;);if(a&gt;0){b=substr($0,a+6);print substr(b, 0, index(b, &quot; &quot;))}}'</span>
    <span style="color: #c20cb9; font-weight: bold;">gawk</span> <span style="color: #ff0000;">'BEGIN{sum=0}{sum+=$1}END{print sum}'</span> data.txt</pre></td></tr></table><p class="theCode" style="display:none;">gawk -F'|' 'BEGIN {OFS=&quot;|&quot;}{print $1,$2,$3}'
    gawk '{a=index($0, &quot; from &quot;);if(a&gt;0){b=substr($0,a+6);print substr(b, 0, index(b, &quot; &quot;))}}'
    gawk 'BEGIN{sum=0}{sum+=$1}END{print sum}' data.txt</p></div>
    ";i:14;s:557:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #c20cb9; font-weight: bold;">cat</span> <span style="color: #000000; font-weight: bold;">&lt;&lt;</span><span style="color: #ff0000;">'EOF'</span> <span style="color: #000000; font-weight: bold;">&gt;&gt;</span> .<span style="color: #000000; font-weight: bold;">/</span>test.txt
    XXX
    EOF</pre></td></tr></table><p class="theCode" style="display:none;">cat &lt;&lt;'EOF' &gt;&gt; ./test.txt
    XXX
    EOF</p></div>
    ";i:15;s:1832:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;">接收方 
    <span style="color: #000000; font-weight: bold;">/</span>sbin<span style="color: #000000; font-weight: bold;">/</span><span style="color: #c20cb9; font-weight: bold;">ifconfig</span> <span style="color: #000000; font-weight: bold;">|</span><span style="color: #c20cb9; font-weight: bold;">grep</span> <span style="color: #ff0000;">'inet addr:10'</span>
     nc <span style="color: #660033;">-l</span> <span style="color: #000000;">9999</span> <span style="color: #000000; font-weight: bold;">|</span> <span style="color: #c20cb9; font-weight: bold;">tar</span> zxvf -
    发送方 <span style="color: #c20cb9; font-weight: bold;">tar</span> czvf - .<span style="color: #000000; font-weight: bold;">/</span>xxx <span style="color: #000000; font-weight: bold;">|</span> nc server <span style="color: #000000;">9999</span>
    &nbsp;
    如果nc -l执行失败，下载旧版本 http:<span style="color: #000000; font-weight: bold;">//</span>vault.centos.org<span style="color: #000000; font-weight: bold;">/</span><span style="color: #000000;">6.6</span><span style="color: #000000; font-weight: bold;">/</span>os<span style="color: #000000; font-weight: bold;">/</span>x86_64<span style="color: #000000; font-weight: bold;">/</span>Packages<span style="color: #000000; font-weight: bold;">/</span>nc-<span style="color: #000000;">1.84</span>-<span style="color: #000000;">22</span>.el6.x86_64.rpm</pre></td></tr></table><p class="theCode" style="display:none;">接收方 
    /sbin/ifconfig |grep 'inet addr:10'
     nc -l 9999 | tar zxvf -
    发送方 tar czvf - ./xxx | nc server 9999
    
    如果nc -l执行失败，下载旧版本 http://vault.centos.org/6.6/os/x86_64/Packages/nc-1.84-22.el6.x86_64.rpm</p></div>
    ";i:16;s:1097:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #c20cb9; font-weight: bold;">find</span> <span style="color: #000000; font-weight: bold;">/</span>tmp<span style="color: #000000; font-weight: bold;">/</span> <span style="color: #660033;">-mtime</span> +<span style="color: #000000;">1</span> <span style="color: #660033;">-name</span> <span style="color: #ff0000;">'xxx_*.log'</span> <span style="color: #660033;">-delete</span>
    <span style="color: #c20cb9; font-weight: bold;">find</span> <span style="color: #000000; font-weight: bold;">/</span>tmp<span style="color: #000000; font-weight: bold;">/</span> <span style="color: #660033;">-mmin</span> +<span style="color: #000000;">60</span> <span style="color: #660033;">-name</span> <span style="color: #ff0000;">'xxx_*.log'</span> <span style="color: #660033;">-delete</span></pre></td></tr></table><p class="theCode" style="display:none;">find /tmp/ -mtime +1 -name 'xxx_*.log' -delete
    find /tmp/ -mmin +60 -name 'xxx_*.log' -delete</p></div>
    ";i:17;s:528:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #007800;">dt</span>=$<span style="color: #7a0874; font-weight: bold;">&#40;</span><span style="color: #c20cb9; font-weight: bold;">date</span> +<span style="color: #ff0000;">&quot;%Y%m%d_%H%M%S&quot;</span><span style="color: #7a0874; font-weight: bold;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">dt=$(date +&quot;%Y%m%d_%H%M%S&quot;)</p></div>
    ";i:18;s:432:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #666666; font-style: italic;"># 把xxx加入apache组</span>
    usermod <span style="color: #660033;">-a</span> <span style="color: #660033;">-G</span> apache xxx</pre></td></tr></table><p class="theCode" style="display:none;"># 把xxx加入apache组
    usermod -a -G apache xxx</p></div>
    ";i:19;s:1591:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #666666; font-style: italic;"># 按human readable 方式排序（sort -h）</span>
    hdfs dfs <span style="color: #660033;">-du</span> <span style="color: #660033;">-h</span> <span style="color: #000000; font-weight: bold;">/</span>user<span style="color: #000000; font-weight: bold;">/|</span><span style="color: #c20cb9; font-weight: bold;">sed</span> <span style="color: #660033;">-r</span> <span style="color: #ff0000;">'s/([0-9.]*)[ ]/\1/'</span><span style="color: #000000; font-weight: bold;">|</span><span style="color: #c20cb9; font-weight: bold;">sort</span> <span style="color: #660033;">-hr</span>
    &nbsp;
    <span style="color: #666666; font-style: italic;"># -t是分隔符</span>
    <span style="color: #666666; font-style: italic;"># 先按第一列排序，再按第二列数字排序</span>
    <span style="color: #c20cb9; font-weight: bold;">cat</span> <span style="color: #000000;">1</span>.txt <span style="color: #000000; font-weight: bold;">|</span><span style="color: #c20cb9; font-weight: bold;">sort</span> <span style="color: #660033;">-t</span><span style="color: #ff0000;">','</span> -k1,<span style="color: #000000;">1</span> -k2,2n</pre></td></tr></table><p class="theCode" style="display:none;"># 按human readable 方式排序（sort -h）
    hdfs dfs -du -h /user/|sed -r 's/([0-9.]*)[ ]/\1/'|sort -hr
    
    # -t是分隔符
    # 先按第一列排序，再按第二列数字排序
    cat 1.txt |sort -t',' -k1,1 -k2,2n</p></div>
    ";i:20;s:1037:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #c20cb9; font-weight: bold;">head</span> 000000_0 <span style="color: #000000; font-weight: bold;">|</span><span style="color: #c20cb9; font-weight: bold;">awk</span> <span style="color: #660033;">-v</span> <span style="color: #007800;">RS</span>=<span style="color: #ff0000;">'`'</span> <span style="color: #660033;">-F</span><span style="color: #ff0000;">'='</span> <span style="color: #ff0000;">'$1==&quot;keyname&quot;'</span>
    <span style="color: #c20cb9; font-weight: bold;">head</span> 000000_0 <span style="color: #000000; font-weight: bold;">|</span><span style="color: #c20cb9; font-weight: bold;">grep</span> <span style="color: #660033;">-o</span> <span style="color: #ff0000;">'`keyname=[^`]*'</span></pre></td></tr></table><p class="theCode" style="display:none;">head 000000_0 |awk -v RS='`' -F'=' '$1==&quot;keyname&quot;'
    head 000000_0 |grep -o '`keyname=[^`]*'</p></div>
    ";i:21;s:897:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #666666; font-style: italic;"># 把dir1的目录结构复制到dir2内 </span>
    <span style="color: #c20cb9; font-weight: bold;">find</span> .<span style="color: #000000; font-weight: bold;">/</span>dir1 <span style="color: #660033;">-type</span> d <span style="color: #660033;">-exec</span> <span style="color: #c20cb9; font-weight: bold;">mkdir</span> <span style="color: #660033;">-p</span> dir2<span style="color: #000000; font-weight: bold;">/</span>\<span style="color: #7a0874; font-weight: bold;">&#123;</span>\<span style="color: #7a0874; font-weight: bold;">&#125;</span> \;</pre></td></tr></table><p class="theCode" style="display:none;"># 把dir1的目录结构复制到dir2内 
    find ./dir1 -type d -exec mkdir -p dir2/\{\} \;</p></div>
    ";i:22;s:3752:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;">retry<span style="color: #7a0874; font-weight: bold;">&#40;</span><span style="color: #7a0874; font-weight: bold;">&#41;</span> <span style="color: #7a0874; font-weight: bold;">&#123;</span>
        <span style="color: #7a0874; font-weight: bold;">local</span> <span style="color: #660033;">-r</span> <span style="color: #660033;">-i</span> <span style="color: #007800;">max_attempts</span>=<span style="color: #ff0000;">&quot;$1&quot;</span>; <span style="color: #7a0874; font-weight: bold;">shift</span>
        <span style="color: #7a0874; font-weight: bold;">local</span> <span style="color: #660033;">-r</span> <span style="color: #007800;">cmd</span>=<span style="color: #ff0000;">&quot;$@&quot;</span>
        <span style="color: #7a0874; font-weight: bold;">local</span> <span style="color: #660033;">-i</span> <span style="color: #007800;">attempt_num</span>=<span style="color: #000000;">1</span>
    &nbsp;
        <span style="color: #000000; font-weight: bold;">until</span> <span style="color: #007800;">$cmd</span>
        <span style="color: #000000; font-weight: bold;">do</span>
            <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #7a0874; font-weight: bold;">&#40;</span><span style="color: #7a0874; font-weight: bold;">&#40;</span> attempt_num == max_attempts <span style="color: #7a0874; font-weight: bold;">&#41;</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
            <span style="color: #000000; font-weight: bold;">then</span>
                <span style="color: #7a0874; font-weight: bold;">echo</span> <span style="color: #ff0000;">&quot;Attempt <span style="color: #007800;">$attempt_num</span> failed and there are no more attempts left!&quot;</span>
                <span style="color: #7a0874; font-weight: bold;">return</span> <span style="color: #000000;">1</span>
            <span style="color: #000000; font-weight: bold;">else</span>
                <span style="color: #7a0874; font-weight: bold;">echo</span> <span style="color: #ff0000;">&quot;Attempt <span style="color: #007800;">$attempt_num</span> failed! Trying again in 60 seconds...&quot;</span>
                <span style="color: #7a0874; font-weight: bold;">echo</span> $<span style="color: #7a0874; font-weight: bold;">&#40;</span><span style="color: #7a0874; font-weight: bold;">&#40;</span> attempt_num++ <span style="color: #7a0874; font-weight: bold;">&#41;</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
                <span style="color: #c20cb9; font-weight: bold;">sleep</span> <span style="color: #000000;">60</span>
            <span style="color: #000000; font-weight: bold;">fi</span>
        <span style="color: #000000; font-weight: bold;">done</span>
    <span style="color: #7a0874; font-weight: bold;">&#125;</span>
    &nbsp;
    <span style="color: #666666; font-style: italic;"># 使用方式</span>
    retry <span style="color: #000000;">6</span> <span style="color: #7a0874; font-weight: bold;">echo</span> <span style="color: #ff0000;">&quot;ok&quot;</span></pre></td></tr></table><p class="theCode" style="display:none;">retry() {
        local -r -i max_attempts=&quot;$1&quot;; shift
        local -r cmd=&quot;$@&quot;
        local -i attempt_num=1
    
        until $cmd
        do
            if (( attempt_num == max_attempts ))
            then
                echo &quot;Attempt $attempt_num failed and there are no more attempts left!&quot;
                return 1
            else
                echo &quot;Attempt $attempt_num failed! Trying again in 60 seconds...&quot;
                echo $(( attempt_num++ ))
                sleep 60
            fi
        done
    }
    
    # 使用方式
    retry 6 echo &quot;ok&quot;</p></div>
    ";}
categories:
  - Linux
tags:
  - Linux
  - linux shell
  - shell

---
## 日期

# 取前一天

date -d &#8216;1 days ago&#8217; +%Y-%m-%d
## 命令別名設定功能： (alias)

alias ll=&#8217;ls -al&#8217;
## 一些特殊值

$$：(關於本 shell 的 PID)  
$!：得到子进程的进程PID,例如nohup的命令可以通过这个获取PID  
$?：(關於上個執行指令的回傳值)  
$#: 参数个数
$@ ：代表『 &#8220;$1&#8221; &#8220;$2&#8221; &#8220;$3&#8221; &#8220;$4&#8221; 』  
$* ：代表『 &#8220;$1c$2c$3c$4&#8221; 』，其中 c 為分隔字元
## declare

数值计算要用 declare -i sum=100+12  
也可以用sum=$((100+12))计算  
[root@www ~]# declare [-aixr] variable  
選項與參數：  
-a ：將後面名為 variable 的變數定義成為陣列 (array) 類型  
-i ：將後面名為 variable 的變數定義成為整數數字 (integer) 類型  
-x ：用法與 export 一樣，就是將後面的 variable 變成環境變數；  
-r ：將變數設定成為 readonly 類型，該變數不可被更改內容，也不能 unset
## 数组

var[1]=&#8221;small min&#8221;  
echo $(var[1])
## 截取字符串

<pre lang="bash" escaped="true"># 从第0位开始截取2个字符
echo ${a:0:2}</pre>
## 删除/替换字符

echo ${PATH#/usr_:} #从前到后开始删除掉第一个符合条件的字符  
echo ${PATH##/usr_:} #从前到后开始删除掉所有符合条件的字符  
也可以从后面开始，就是把#号替换成%号  
echo ${PATH/usr/USR} #替换  
echo ${PATH//usr/USR} #替换所有
## &&和||

可以把多条命令串起来，例如  
ls ./test/||mkdir ./test/ #如果目录不存在，创建一个
## 判断

使用中括号时注意空格必须要有[ -e &#8220;xxx&#8221; ]
语法
<pre lang="bash">if [ "$name" == "Fatkun" ]; then
    echo "Hi!Fatkun"
elif [ ... ]; then
    echo "..."
else
    echo "..."
fi</pre>
&nbsp;
<table style="width: 85%;" border="1" cellspacing="0" cellpadding="3" bgcolor="lightyellow">  <tr align="center" bgcolor="lightblue">    <td width="100">      測試的標誌    </td>
    <td>      代表意義    </td>  </tr>
  <tr bgcolor="lightblue">    <td colspan="2">      1. 關於某個檔名的『檔案類型』判斷，如 test -e filename 表示存在否    </td>  </tr>
  <tr>    <td align="center">      -e    </td>
    <td>      該『檔名』是否存在？(常用)    </td>  </tr>
  <tr>    <td align="center">      -f    </td>
    <td>      該『檔名』是否存在且為檔案(file)？(常用)    </td>  </tr>
  <tr>    <td align="center">      -d    </td>
    <td>      該『檔名』是否存在且為目錄(directory)？(常用)    </td>  </tr>
  <tr>    <td align="center">      -b    </td>
    <td>      該『檔名』是否存在且為一個 block device 裝置？    </td>  </tr>
  <tr>    <td align="center">      -c    </td>
    <td>      該『檔名』是否存在且為一個 character device 裝置？    </td>  </tr>
  <tr>    <td align="center">      -S    </td>
    <td>      該『檔名』是否存在且為一個 Socket 檔案？    </td>  </tr>
  <tr>    <td align="center">      -p    </td>
    <td>      該『檔名』是否存在且為一個 FIFO (pipe) 檔案？    </td>  </tr>
  <tr>    <td align="center">      -L    </td>
    <td>      該『檔名』是否存在且為一個連結檔？    </td>  </tr>
  <tr bgcolor="lightblue">    <td colspan="2">      2. 關於檔案的權限偵測，如 test -r filename 表示可讀否 (但 root 權限常有例外)    </td>  </tr>
  <tr>    <td align="center">      -r    </td>
    <td>      偵測該檔名是否存在且具有『可讀』的權限？    </td>  </tr>
  <tr>    <td align="center">      -w    </td>
    <td>      偵測該檔名是否存在且具有『可寫』的權限？    </td>  </tr>
  <tr>    <td align="center">      -x    </td>
    <td>      偵測該檔名是否存在且具有『可執行』的權限？    </td>  </tr>
  <tr>    <td align="center">      -u    </td>
    <td>      偵測該檔名是否存在且具有『SUID』的屬性？    </td>  </tr>
  <tr>    <td align="center">      -g    </td>
    <td>      偵測該檔名是否存在且具有『SGID』的屬性？    </td>  </tr>
  <tr>    <td align="center">      -k    </td>
    <td>      偵測該檔名是否存在且具有『Sticky bit』的屬性？    </td>  </tr>
  <tr>    <td align="center">      -s    </td>
    <td>      偵測該檔名是否存在且為『非空白檔案』？    </td>  </tr>
  <tr bgcolor="lightblue">    <td colspan="2">      3. 兩個檔案之間的比較，如： test file1 -nt file2    </td>  </tr>
  <tr>    <td align="center">      -nt    </td>
    <td>      (newer than)判斷 file1 是否比 file2 新    </td>  </tr>
  <tr>    <td align="center">      -ot    </td>
    <td>      (older than)判斷 file1 是否比 file2 舊    </td>  </tr>
  <tr>    <td align="center">      -ef    </td>
    <td>      判斷 file1 與 file2 是否為同一檔案，可用在判斷 hard link 的判定上。 主要意義在判定，兩個檔案是否均指向同一個 inode 哩！    </td>  </tr>
  <tr bgcolor="lightblue">    <td colspan="2">      4. 關於兩個整數之間的判定，例如 test n1 -eq n2    </td>  </tr>
  <tr>    <td align="center">      -eq    </td>
    <td>      兩數值相等 (equal)    </td>  </tr>
  <tr>    <td align="center">      -ne    </td>
    <td>      兩數值不等 (not equal)    </td>  </tr>
  <tr>    <td align="center">      -gt    </td>
    <td>      n1 大於 n2 (greater than)    </td>  </tr>
  <tr>    <td align="center">      -lt    </td>
    <td>      n1 小於 n2 (less than)    </td>  </tr>
  <tr>    <td align="center">      -ge    </td>
    <td>      n1 大於等於 n2 (greater than or equal)    </td>  </tr>
  <tr>    <td align="center">      -le    </td>
    <td>      n1 小於等於 n2 (less than or equal)    </td>  </tr>
  <tr bgcolor="lightblue">    <td colspan="2">      5. 判定字串的資料    </td>  </tr>
  <tr>    <td align="center">      test -z string    </td>
    <td>      判定字串是否為 0 ？若 string 為空字串，則為 true    </td>  </tr>
  <tr>    <td align="center">      test -n string    </td>
    <td>      判定字串是否非為 0 ？若 string 為空字串，則為 false。<br /> 註： -n 亦可省略    </td>  </tr>
  <tr>    <td align="center">      test str1 = str2    </td>
    <td>      判定 str1 是否等於 str2 ，若相等，則回傳 true    </td>  </tr>
  <tr>    <td align="center">      test str1 != str2    </td>
    <td>      判定 str1 是否不等於 str2 ，若相等，則回傳 false    </td>  </tr>
  <tr bgcolor="lightblue">    <td colspan="2">      6. 多重條件判定，例如： test -r filename -a -x filename    </td>  </tr>
  <tr>    <td align="center">      -a    </td>
    <td>      (and)兩狀況同時成立！例如 test -r file -a -x file，則 file 同時具有 r 與 x 權限時，才回傳 true。    </td>  </tr>
  <tr>    <td align="center">      -o    </td>
    <td>      (or)兩狀況任何一個成立！例如 test -r file -o -x file，則 file 具有 r 或 x 權限時，就可回傳 true。    </td>  </tr>
  <tr>    <td align="center">      !    </td>
    <td>      反相狀態，如 test ! -x file ，當 file 不具有 x 時，回傳 true    </td>  </tr></table>
## case语法

<pre lang="bash" escaped="true">case  $變數名稱 in   &lt;==關鍵字為 case ，還有變數前有錢字號
  "第一個變數內容")   &lt;==每個變數內容建議用雙引號括起來，關鍵字則為小括號 )
    程式段
    ;;            &lt;==每個類別結尾使用兩個連續的分號來處理！
  "第二個變數內容")
    程式段
    ;;
  *)                  &lt;==最後一個變數內容都會用 * 來代表所有其他值
    不包含第一個變數內容與第二個變數內容的其他程式執行段
    exit 1
    ;;
esac                  &lt;==最終的 case 結尾！『反過來寫』思考一下！</pre>
## while语法

<pre lang="bash" escaped="true">while [ condition ]  &lt;==中括號內的狀態就是判斷式
do            &lt;==do 是迴圈的開始！
    程式段落
done          &lt;==done 是迴圈的結束</pre>
## for&#8230;do&#8230;done语法

<pre lang="bash" escaped="true">for var in con1 con2 con3 ...
do
    程式段
done</pre>
<pre escaped="true" lang="bash">CLUSTERS=(aaa bbb ccc)
for cluster in ${CLUSTERS[@]};
do
    echo $cluster
done</pre>
<pre lang="bash" escaped="true">for((i=1;i&lt;100;i++));do
echo $i
done</pre>
## 软链接替换

ln -snf ./hive-0.7.1/ hive
## 利用grep和gawk，xargs来kill

xargs会把gawk的每一行变成kill的参数，如 kill 1 2 3
grep -v 是排除
ps -ef|grep scott|grep -v grep|gawk {&#8216;print $1&#8217;}|xargs kill
## sed命令替换文本

<pre lang="bash" escaped="true">sed -i "s/oldstring/newstring/g" file #在原文件修改
sed "s/oldstring/newstring/g" file &gt;file.new # 输出到其他文件
file="/tmp/crontab_`date +"%H%M%S"`.bak"; crontab -l &gt; $file; sed "s/\*\/5 \* \* \* \* run-parts/\* \* \* \* \* run-parts/g" $file &gt; "$file.new"; crontab "$file.new"; # 替换crontab文件
sed -r 's/^\s+([0-9]+) /\1|/g'
sed -i '$i\eeeeeeeee'  urfile # 在倒数一行插入内容</pre>
## tar

<pre lang="bash">tar --exclude=log -cvzf xxx_`date +"%Y-%m-%d_%H_%M"`.tar.gz ./xxx
# 使用xz压缩，如果使用lzma压缩也是用XZ_OPT
XZ_OPT=-1 tar -cf 1.tar.xz --xz xx.log
</pre>
## 获取机器IP

via:http://www.cnblogs.com/starspace/archive/2009/02/13/1390062.html
<pre lang="bash" escaped="true">/sbin/ifconfig -a|grep inet|grep -v 127.0.0.1|grep -v inet6|awk '{print $2}'|tr -d "addr:"</pre>
## GREP 获取前几行后几行的内容

<pre lang="html">grep -n -B1 -A1 "关键字" file  #匹配关键字的前一行与后一行.</pre>
## Rsync 通过ssh传输

<pre lang="bash"># -e 参数指定用ssh传输
rsync --exclude 'logs' --size-only --progress -rave "ssh -p2222" /home/xx/ 用户名@IP地址:/tmp/xx</pre>
## kill进程树

<http://stackoverflow.com/questions/392022/best-way-to-kill-all-child-processes>
## gawk

<pre lang="bash" escaped="true">gawk -F'|' 'BEGIN {OFS="|"}{print $1,$2,$3}'
gawk '{a=index($0, " from ");if(a&gt;0){b=substr($0,a+6);print substr(b, 0, index(b, " "))}}'
gawk 'BEGIN{sum=0}{sum+=$1}END{print sum}' data.txt
</pre>
## 输出一大段文本

<pre lang="bash" escaped="true">cat &lt;&lt;'EOF' &gt;&gt; ./test.txt
XXX
EOF</pre>
## 简单的http服务

<p lang="bash">  python -m SimpleHTTPServer 8080</p>
## NC传文件

<pre lang="bash" escaped="true">接收方 
/sbin/ifconfig |grep 'inet addr:10'
 nc -l 9999 | tar zxvf -
发送方 tar czvf - ./xxx | nc server 9999

如果nc -l执行失败，下载旧版本 http://vault.centos.org/6.6/os/x86_64/Packages/nc-1.84-22.el6.x86_64.rpm
</pre>
## Find

<pre lang="bash">find /tmp/ -mtime +1 -name 'xxx_*.log' -delete
find /tmp/ -mmin +60 -name 'xxx_*.log' -delete
</pre>
## date

<pre lang="bash">dt=$(date +"%Y%m%d_%H%M%S")</pre>
## 用户/组管理命令

<http://cnzhx.net/blog/linux-add-user-to-group/>
<pre lang="bash"># 把xxx加入apache组
usermod -a -G apache xxx
</pre>
## sort

<pre lang="bash" escaped="true"># 按human readable 方式排序（sort -h）
hdfs dfs -du -h /user/|sed -r 's/([0-9.]*)[ ]/\1/'|sort -hr

# -t是分隔符
# 先按第一列排序，再按第二列数字排序
cat 1.txt |sort -t',' -k1,1 -k2,2n
</pre>
## 截取kv文件

[via][1]
<pre lang="bash" escaped="true">head 000000_0 |awk -v RS='`' -F'=' '$1=="keyname"'
head 000000_0 |grep -o '`keyname=[^`]*'</pre>
## 只复制目录结构

<pre lang="bash" escaped="true"># 把dir1的目录结构复制到dir2内 
find ./dir1 -type d -exec mkdir -p dir2/\{\} \;</pre>
## shell重试方法

<pre lang="bash" escaped="true">retry() {
    local -r -i max_attempts="$1"; shift
    local -r cmd="$@"
    local -i attempt_num=1

    until $cmd
    do
        if (( attempt_num == max_attempts ))
        then
            echo "Attempt $attempt_num failed and there are no more attempts left!"
            return 1
        else
            echo "Attempt $attempt_num failed! Trying again in 60 seconds..."
            echo $(( attempt_num++ ))
            sleep 60
        fi
    done
}

# 使用方式
retry 6 echo "ok"</pre>
## 参考

大部分内容来自：http://linux.vbird.org/linux_basic/0320bash.php  
[linux命令行查询][2]

 [1]: http://unix.stackexchange.com/questions/186453/cut-for-key-value-pairs
 [2]: http://man.linuxde.net/