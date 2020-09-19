---
title: golang for 循环指针的坑
author: fatkun
type: post
date: 2019-08-01T06:09:46+00:00
url: /2019/08/golang-for-pointer-error.html
wp-syntax-cache-content:
  - |
    a:2:{i:1;s:1874:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="other" style="font-family:monospace;">package main
    &nbsp;
    import (
        &quot;log&quot;
        &quot;time&quot;
    )
    &nbsp;
    type student struct {
        Name string
        Age  int
    }
    &nbsp;
    func main() {
        m := make([]*student, 3)
        stus := []student{
            student{Name: &quot;sa&quot;, Age: 10},
            student{Name: &quot;sb&quot;, Age: 11},
            student{Name: &quot;sc&quot;, Age: 12},
        }
    &nbsp;
        log.Println(&quot;################ 错误做法 ##################&quot;)
        for k, stu := range stus {
            m[k] = &amp;stu
        }
        for _, s := range m {
            log.Println(s.Name, s.Age)
        }
    &nbsp;
        log.Println(&quot;################ 正确做法 ##################&quot;)
        for k, _ := range stus {
            m[k] = &amp;stus[k]
        }
        for _, s := range m {
            log.Println(s.Name, s.Age)
        }
        time.Sleep(2 * time.Second)
    }</pre></td></tr></table><p class="theCode" style="display:none;">package main
    
    import (
        &quot;log&quot;
        &quot;time&quot;
    )
    
    type student struct {
        Name string
        Age  int
    }
    
    func main() {
        m := make([]*student, 3)
        stus := []student{
            student{Name: &quot;sa&quot;, Age: 10},
            student{Name: &quot;sb&quot;, Age: 11},
            student{Name: &quot;sc&quot;, Age: 12},
        }
    
        log.Println(&quot;################ 错误做法 ##################&quot;)
        for k, stu := range stus {
            m[k] = &amp;stu
        }
        for _, s := range m {
            log.Println(s.Name, s.Age)
        }
    
        log.Println(&quot;################ 正确做法 ##################&quot;)
        for k, _ := range stus {
            m[k] = &amp;stus[k]
        }
        for _, s := range m {
            log.Println(s.Name, s.Age)
        }
        time.Sleep(2 * time.Second)
    }</p></div>
    ";i:2;s:805:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="other" style="font-family:monospace;">2018/12/12 12:24:19 ################ 错误做法 ##################
    2018/12/12 12:24:19 sc 12
    2018/12/12 12:24:19 sc 12
    2018/12/12 12:24:19 sc 12
    2018/12/12 12:24:19 ################ 正确做法 ##################
    2018/12/12 12:24:19 sa 10
    2018/12/12 12:24:19 sb 11
    2018/12/12 12:24:19 sc 12</pre></td></tr></table><p class="theCode" style="display:none;">2018/12/12 12:24:19 ################ 错误做法 ##################
    2018/12/12 12:24:19 sc 12
    2018/12/12 12:24:19 sc 12
    2018/12/12 12:24:19 sc 12
    2018/12/12 12:24:19 ################ 正确做法 ##################
    2018/12/12 12:24:19 sa 10
    2018/12/12 12:24:19 sb 11
    2018/12/12 12:24:19 sc 12</p></div>
    ";}
categories:
  - go

---
原文：<https://www.jianshu.com/p/dbd81a7c2bcb>
<pre lang="other" escaped="true">package main

import (
    "log"
    "time"
)

type student struct {
    Name string
    Age  int
}

func main() {
    m := make([]*student, 3)
    stus := []student{
        student{Name: "sa", Age: 10},
        student{Name: "sb", Age: 11},
        student{Name: "sc", Age: 12},
    }

    log.Println("################ 错误做法 ##################")
    for k, stu := range stus {
        m[k] = &stu
    }
    for _, s := range m {
        log.Println(s.Name, s.Age)
    }

    log.Println("################ 正确做法 ##################")
    for k, _ := range stus {
        m[k] = &stus[k]
    }
    for _, s := range m {
        log.Println(s.Name, s.Age)
    }
    time.Sleep(2 * time.Second)
}</pre>
输出如下：
<pre lang="other" escaped="true">2018/12/12 12:24:19 ################ 错误做法 ##################
2018/12/12 12:24:19 sc 12
2018/12/12 12:24:19 sc 12
2018/12/12 12:24:19 sc 12
2018/12/12 12:24:19 ################ 正确做法 ##################
2018/12/12 12:24:19 sa 10
2018/12/12 12:24:19 sb 11
2018/12/12 12:24:19 sc 12
</pre>
for k, stu := range stus 变量stu 的地址并不会随着遍历而改变，所以&stu 对应的值始终为stus的最后的元素