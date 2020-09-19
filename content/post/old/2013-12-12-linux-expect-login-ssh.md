---
title: linux expect自动登录ssh
author: fatkun
type: post
date: 2013-12-12T12:00:40+00:00
url: /2013/12/linux-expect-login-ssh.html
duoshuo_thread_id:
  - 6300410060849808130
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:5620:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #666666; font-style: italic;">#!/usr/bin/expect</span>
    <span style="color: #666666; font-style: italic;"># 传送文件并且执行</span>
    <span style="color: #000000; font-weight: bold;">set</span> timeout <span style="color: #000000;">30</span>
    &nbsp;
    <span style="color: #000000; font-weight: bold;">set</span> host <span style="color: #7a0874; font-weight: bold;">&#91;</span>lindex <span style="color: #007800;">$argv</span> <span style="color: #000000;">0</span><span style="color: #7a0874; font-weight: bold;">&#93;</span>
    <span style="color: #000000; font-weight: bold;">set</span> username <span style="color: #7a0874; font-weight: bold;">&#91;</span>lindex <span style="color: #007800;">$argv</span> <span style="color: #000000;">1</span><span style="color: #7a0874; font-weight: bold;">&#93;</span>
    <span style="color: #000000; font-weight: bold;">set</span> password <span style="color: #7a0874; font-weight: bold;">&#91;</span>lindex <span style="color: #007800;">$argv</span> <span style="color: #000000;">2</span><span style="color: #7a0874; font-weight: bold;">&#93;</span>
    <span style="color: #000000; font-weight: bold;">set</span> <span style="color: #c20cb9; font-weight: bold;">file</span> <span style="color: #7a0874; font-weight: bold;">&#91;</span>lindex <span style="color: #007800;">$argv</span> <span style="color: #000000;">3</span><span style="color: #7a0874; font-weight: bold;">&#93;</span>
    <span style="color: #000000; font-weight: bold;">set</span> center_password <span style="color: #7a0874; font-weight: bold;">&#91;</span>lindex <span style="color: #007800;">$argv</span> <span style="color: #000000;">4</span><span style="color: #7a0874; font-weight: bold;">&#93;</span>
    &nbsp;
    spawn <span style="color: #c20cb9; font-weight: bold;">scp</span> <span style="color: #660033;">-P22</span> <span style="color: #007800;">$file</span> <span style="color: #007800;">$username</span><span style="color: #000000; font-weight: bold;">@</span><span style="color: #007800;">$host</span>:<span style="color: #000000; font-weight: bold;">/</span>tmp<span style="color: #000000; font-weight: bold;">/</span>tmp.sh
    <span style="color: #c20cb9; font-weight: bold;">sleep</span> <span style="color: #000000;">1</span>
    expect <span style="color: #7a0874; font-weight: bold;">&#123;</span>
     <span style="color: #ff0000;">&quot;*yes/no*&quot;</span> <span style="color: #7a0874; font-weight: bold;">&#123;</span>send <span style="color: #ff0000;">&quot;yes<span style="color: #000099; font-weight: bold;">\n</span>&quot;</span>; exp_continue<span style="color: #7a0874; font-weight: bold;">&#125;</span>
     <span style="color: #ff0000;">&quot;*password:*&quot;</span> <span style="color: #7a0874; font-weight: bold;">&#123;</span>send <span style="color: #ff0000;">&quot;<span style="color: #007800;">$password</span><span style="color: #000099; font-weight: bold;">\n</span>&quot;</span> <span style="color: #7a0874; font-weight: bold;">&#125;</span>
     <span style="color: #7a0874; font-weight: bold;">&#125;</span>
    interact
    &nbsp;
    spawn <span style="color: #c20cb9; font-weight: bold;">ssh</span> <span style="color: #660033;">-p22</span> <span style="color: #007800;">$username</span><span style="color: #000000; font-weight: bold;">@</span><span style="color: #007800;">$host</span>
    <span style="color: #c20cb9; font-weight: bold;">sleep</span> <span style="color: #000000;">1</span>
    expect <span style="color: #7a0874; font-weight: bold;">&#123;</span>
     <span style="color: #ff0000;">&quot;*yes/no*&quot;</span> <span style="color: #7a0874; font-weight: bold;">&#123;</span>send <span style="color: #ff0000;">&quot;yes<span style="color: #000099; font-weight: bold;">\n</span>&quot;</span>; exp_continue<span style="color: #7a0874; font-weight: bold;">&#125;</span>
     <span style="color: #ff0000;">&quot;*password:*&quot;</span> <span style="color: #7a0874; font-weight: bold;">&#123;</span>send <span style="color: #ff0000;">&quot;<span style="color: #007800;">$password</span><span style="color: #000099; font-weight: bold;">\n</span>&quot;</span> <span style="color: #7a0874; font-weight: bold;">&#125;</span>
     <span style="color: #7a0874; font-weight: bold;">&#125;</span>
    <span style="color: #c20cb9; font-weight: bold;">sleep</span> <span style="color: #000000;">1</span>
    expect <span style="color: #ff0000;">&quot;*$*&quot;</span>
    send <span style="color: #ff0000;">&quot;sh /tmp/tmp.sh <span style="color: #000099; font-weight: bold;">\n</span>&quot;</span>
    send <span style="color: #ff0000;">&quot;exit<span style="color: #000099; font-weight: bold;">\n</span>&quot;</span>
    <span style="color: #666666; font-style: italic;">#interact </span>
    expect eof</pre></td></tr></table><p class="theCode" style="display:none;">#!/usr/bin/expect
    # 传送文件并且执行
    set timeout 30
    
    set host [lindex $argv 0]
    set username [lindex $argv 1]
    set password [lindex $argv 2]
    set file [lindex $argv 3]
    set center_password [lindex $argv 4]
    
    spawn scp -P22 $file $username@$host:/tmp/tmp.sh
    sleep 1
    expect {
     &quot;*yes/no*&quot; {send &quot;yes\n&quot;; exp_continue}
     &quot;*password:*&quot; {send &quot;$password\n&quot; }
     }
    interact
    
    spawn ssh -p22 $username@$host
    sleep 1
    expect {
     &quot;*yes/no*&quot; {send &quot;yes\n&quot;; exp_continue}
     &quot;*password:*&quot; {send &quot;$password\n&quot; }
     }
    sleep 1
    expect &quot;*$*&quot;
    send &quot;sh /tmp/tmp.sh \n&quot;
    send &quot;exit\n&quot;
    #interact 
    expect eof</p></div>
    ";}
categories:
  - Linux
tags:
  - expect
  - Linux

---
&nbsp;
<pre lang="bash" escaped="true">#!/usr/bin/expect
# 传送文件并且执行
set timeout 30

set host [lindex $argv 0]
set username [lindex $argv 1]
set password [lindex $argv 2]
set file [lindex $argv 3]
set center_password [lindex $argv 4]

spawn scp -P22 $file $username@$host:/tmp/tmp.sh
sleep 1
expect {
 "*yes/no*" {send "yes\n"; exp_continue}
 "*password:*" {send "$password\n" }
 }
interact

spawn ssh -p22 $username@$host
sleep 1
expect {
 "*yes/no*" {send "yes\n"; exp_continue}
 "*password:*" {send "$password\n" }
 }
sleep 1
expect "*$*"
send "sh /tmp/tmp.sh \n"
send "exit\n"
#interact 
expect eof</pre>
&nbsp;
&nbsp;
## 参考

<http://blog.51yip.com/linux/1462.html>