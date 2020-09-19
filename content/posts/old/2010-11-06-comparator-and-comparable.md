---
title: Comparator和Comparable的区别使用
author: fatkun
type: post
date: 2010-11-06T15:47:58+00:00
url: /2010/11/comparator-and-comparable.html
duoshuo_thread_id:
  - 6300408776776221441
wp-syntax-cache-content:
  - |
    a:2:{i:1;s:8795:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="line_numbers"><pre>1
    2
    3
    4
    5
    6
    7
    8
    9
    10
    11
    12
    13
    14
    15
    16
    17
    18
    19
    20
    21
    22
    23
    24
    25
    26
    27
    28
    29
    30
    31
    32
    33
    34
    35
    36
    37
    38
    39
    40
    41
    42
    43
    44
    45
    </pre></td><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">java.util.Arrays</span><span style="color: #339933;">;</span>
    &nbsp;
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">class</span> User <span style="color: #000000; font-weight: bold;">implements</span> <span style="color: #003399;">Comparable</span> <span style="color: #009900;">&#123;</span>
    &nbsp;
      <span style="color: #000000; font-weight: bold;">private</span> <span style="color: #003399;">String</span> id<span style="color: #339933;">;</span>
      <span style="color: #000000; font-weight: bold;">private</span> <span style="color: #000066; font-weight: bold;">int</span> age<span style="color: #339933;">;</span>
    &nbsp;
      <span style="color: #000000; font-weight: bold;">public</span> User<span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span> id, <span style="color: #000066; font-weight: bold;">int</span> age<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
        <span style="color: #000000; font-weight: bold;">this</span>.<span style="color: #006633;">id</span> <span style="color: #339933;">=</span> id<span style="color: #339933;">;</span>
        <span style="color: #000000; font-weight: bold;">this</span>.<span style="color: #006633;">age</span> <span style="color: #339933;">=</span> age<span style="color: #339933;">;</span>
      <span style="color: #009900;">&#125;</span>
    &nbsp;
      <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">int</span> getAge<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
        <span style="color: #000000; font-weight: bold;">return</span> age<span style="color: #339933;">;</span>
      <span style="color: #009900;">&#125;</span>
    &nbsp;
      <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">void</span> setAge<span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">int</span> age<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
        <span style="color: #000000; font-weight: bold;">this</span>.<span style="color: #006633;">age</span> <span style="color: #339933;">=</span> age<span style="color: #339933;">;</span>
      <span style="color: #009900;">&#125;</span>
    &nbsp;
      <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #003399;">String</span> getId<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
        <span style="color: #000000; font-weight: bold;">return</span> id<span style="color: #339933;">;</span>
      <span style="color: #009900;">&#125;</span>
    &nbsp;
      <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">void</span> setId<span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span> id<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
        <span style="color: #000000; font-weight: bold;">this</span>.<span style="color: #006633;">id</span> <span style="color: #339933;">=</span> id<span style="color: #339933;">;</span>
      <span style="color: #009900;">&#125;</span>
    &nbsp;
      <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">int</span> compareTo<span style="color: #009900;">&#40;</span><span style="color: #003399;">Object</span> o<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
        <span style="color: #000000; font-weight: bold;">return</span> <span style="color: #000000; font-weight: bold;">this</span>.<span style="color: #006633;">age</span> <span style="color: #339933;">-</span> <span style="color: #009900;">&#40;</span><span style="color: #009900;">&#40;</span>User<span style="color: #009900;">&#41;</span> o<span style="color: #009900;">&#41;</span>.<span style="color: #006633;">getAge</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
      <span style="color: #009900;">&#125;</span>
    &nbsp;
      <span style="color: #008000; font-style: italic; font-weight: bold;">/**
       * 测试方法
       */</span>
      <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">static</span> <span style="color: #000066; font-weight: bold;">void</span> main<span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span><span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span> args<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
        User<span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span> users <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> User<span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span> <span style="color: #009900;">&#123;</span> <span style="color: #000000; font-weight: bold;">new</span> User<span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;a&quot;</span>, <span style="color: #cc66cc;">30</span><span style="color: #009900;">&#41;</span>, <span style="color: #000000; font-weight: bold;">new</span> User<span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;b&quot;</span>, <span style="color: #cc66cc;">20</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#125;</span><span style="color: #339933;">;</span>
        <span style="color: #003399;">Arrays</span>.<span style="color: #006633;">sort</span><span style="color: #009900;">&#40;</span>users<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #000000; font-weight: bold;">for</span> <span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">int</span> i <span style="color: #339933;">=</span> <span style="color: #cc66cc;">0</span><span style="color: #339933;">;</span> i <span style="color: #339933;">&lt;</span> users.<span style="color: #006633;">length</span><span style="color: #339933;">;</span> i<span style="color: #339933;">++</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
          User user <span style="color: #339933;">=</span> users<span style="color: #009900;">&#91;</span>i<span style="color: #009900;">&#93;</span><span style="color: #339933;">;</span>
          <span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span>user.<span style="color: #006633;">getId</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">+</span> <span style="color: #0000ff;">&quot; &quot;</span> <span style="color: #339933;">+</span> user.<span style="color: #006633;">getAge</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
      <span style="color: #009900;">&#125;</span>
    &nbsp;
    <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">import java.util.Arrays;
    
    public class User implements Comparable {
    
      private String id;
      private int age;
    
      public User(String id, int age) {
        this.id = id;
        this.age = age;
      }
    
      public int getAge() {
        return age;
      }
    
      public void setAge(int age) {
        this.age = age;
      }
    
      public String getId() {
        return id;
      }
    
      public void setId(String id) {
        this.id = id;
      }
    
      public int compareTo(Object o) {
        return this.age - ((User) o).getAge();
      }
    
      /**
       * 测试方法
       */
      public static void main(String[] args) {
        User[] users = new User[] { new User(&quot;a&quot;, 30), new User(&quot;b&quot;, 20) };
        Arrays.sort(users);
        for (int i = 0; i &lt; users.length; i++) {
          User user = users[i];
          System.out.println(user.getId() + &quot; &quot; + user.getAge());
        }
      }
    
    }</p></div>
    ";i:2;s:7072:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="line_numbers"><pre>1
    2
    3
    4
    5
    6
    7
    8
    9
    10
    11
    12
    13
    14
    15
    16
    17
    18
    19
    20
    21
    22
    23
    24
    25
    26
    27
    28
    29
    30
    </pre></td><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">java.util.Arrays</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">java.util.Comparator</span><span style="color: #339933;">;</span>
    &nbsp;
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">class</span> SampleComparator <span style="color: #000000; font-weight: bold;">implements</span> <span style="color: #003399;">Comparator</span> <span style="color: #009900;">&#123;</span>
    &nbsp;
      <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">int</span> compare<span style="color: #009900;">&#40;</span><span style="color: #003399;">Object</span> o1, <span style="color: #003399;">Object</span> o2<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
        <span style="color: #000000; font-weight: bold;">return</span> toInt<span style="color: #009900;">&#40;</span>o1<span style="color: #009900;">&#41;</span> <span style="color: #339933;">-</span> toInt<span style="color: #009900;">&#40;</span>o2<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
      <span style="color: #009900;">&#125;</span>
    &nbsp;
      <span style="color: #000000; font-weight: bold;">private</span> <span style="color: #000066; font-weight: bold;">int</span> toInt<span style="color: #009900;">&#40;</span><span style="color: #003399;">Object</span> o<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
        <span style="color: #003399;">String</span> str <span style="color: #339933;">=</span> <span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span><span style="color: #009900;">&#41;</span> o<span style="color: #339933;">;</span>
        str <span style="color: #339933;">=</span> str.<span style="color: #006633;">replaceAll</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;一&quot;</span>, <span style="color: #0000ff;">&quot;1&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        str <span style="color: #339933;">=</span> str.<span style="color: #006633;">replaceAll</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;二&quot;</span>, <span style="color: #0000ff;">&quot;2&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        str <span style="color: #339933;">=</span> str.<span style="color: #006633;">replaceAll</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;三&quot;</span>, <span style="color: #0000ff;">&quot;3&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #666666; font-style: italic;">//</span>
        <span style="color: #000000; font-weight: bold;">return</span> <span style="color: #003399;">Integer</span>.<span style="color: #006633;">parseInt</span><span style="color: #009900;">&#40;</span>str<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
      <span style="color: #009900;">&#125;</span>
    &nbsp;
      <span style="color: #008000; font-style: italic; font-weight: bold;">/**
       * 测试方法
       */</span>
      <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">static</span> <span style="color: #000066; font-weight: bold;">void</span> main<span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span><span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span> args<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
        <span style="color: #003399;">String</span><span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span> array <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> <span style="color: #003399;">String</span><span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span> <span style="color: #009900;">&#123;</span> <span style="color: #0000ff;">&quot;一二&quot;</span>, <span style="color: #0000ff;">&quot;三&quot;</span>, <span style="color: #0000ff;">&quot;二&quot;</span> <span style="color: #009900;">&#125;</span><span style="color: #339933;">;</span>
        <span style="color: #003399;">Arrays</span>.<span style="color: #006633;">sort</span><span style="color: #009900;">&#40;</span>array, <span style="color: #000000; font-weight: bold;">new</span> SampleComparator<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #000000; font-weight: bold;">for</span> <span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">int</span> i <span style="color: #339933;">=</span> <span style="color: #cc66cc;">0</span><span style="color: #339933;">;</span> i <span style="color: #339933;">&lt;</span> array.<span style="color: #006633;">length</span><span style="color: #339933;">;</span> i<span style="color: #339933;">++</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
          <span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span>array<span style="color: #009900;">&#91;</span>i<span style="color: #009900;">&#93;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
      <span style="color: #009900;">&#125;</span>
    &nbsp;
    <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">import java.util.Arrays;
    import java.util.Comparator;
    
    public class SampleComparator implements Comparator {
    
      public int compare(Object o1, Object o2) {
        return toInt(o1) - toInt(o2);
      }
    
      private int toInt(Object o) {
        String str = (String) o;
        str = str.replaceAll(&quot;一&quot;, &quot;1&quot;);
        str = str.replaceAll(&quot;二&quot;, &quot;2&quot;);
        str = str.replaceAll(&quot;三&quot;, &quot;3&quot;);
        //
        return Integer.parseInt(str);
      }
    
      /**
       * 测试方法
       */
      public static void main(String[] args) {
        String[] array = new String[] { &quot;一二&quot;, &quot;三&quot;, &quot;二&quot; };
        Arrays.sort(array, new SampleComparator());
        for (int i = 0; i &lt; array.length; i++) {
          System.out.println(array[i]);
        }
      }
    
    }</p></div>
    ";}
categories:
  - J2EE
tags:
  - Comparable
  - Comparator
  - java基础

---
## Camparable与Comparator的区别

简单说：
  * 实现Camparable接口可以直接使用sort方法Collections.sort(List list)排序
  * 实现Comparator接口的可以用Collections.sort(List list, Comparator c)排序
一个类实现了Camparable接口则表明这个类的对象之间是可以相互比较的，这个类对象组成的集合就可以**直接使用sort方法**排序。  
Comparator可以看成一种算法的实现，将算法和数据分离，Comparator也可以在下面两种环境下使用：  
1、类的设计师没有考虑到比较问题而没有实现Comparable，可以通过Comparator来实现排序而不必改变对象本身  
2、可以使用多种排序标准，比如升序、降序等
## Camparable实例

<pre escaped="true" lang="java" line="1">import java.util.Arrays;

public class User implements Comparable {

  private String id;
  private int age;

  public User(String id, int age) {
    this.id = id;
    this.age = age;
  }

  public int getAge() {
    return age;
  }

  public void setAge(int age) {
    this.age = age;
  }

  public String getId() {
    return id;
  }

  public void setId(String id) {
    this.id = id;
  }

  public int compareTo(Object o) {
    return this.age - ((User) o).getAge();
  }

  /**
   * 测试方法
   */
  public static void main(String[] args) {
    User[] users = new User[] { new User("a", 30), new User("b", 20) };
    Arrays.sort(users);
    for (int i = 0; i &lt; users.length; i++) {
      User user = users[i];
      System.out.println(user.getId() + " " + user.getAge());
    }
  }

}</pre>
## Comparator实例

<pre escaped="true" lang="java" line="1">import java.util.Arrays;
import java.util.Comparator;

public class SampleComparator implements Comparator {

  public int compare(Object o1, Object o2) {
    return toInt(o1) - toInt(o2);
  }

  private int toInt(Object o) {
    String str = (String) o;
    str = str.replaceAll("一", "1");
    str = str.replaceAll("二", "2");
    str = str.replaceAll("三", "3");
    //
    return Integer.parseInt(str);
  }

  /**
   * 测试方法
   */
  public static void main(String[] args) {
    String[] array = new String[] { "一二", "三", "二" };
    Arrays.sort(array, new SampleComparator());
    for (int i = 0; i &lt; array.length; i++) {
      System.out.println(array[i]);
    }
  }

}</pre>
原文来自：[Comparator和Comparable的区别][1]

 [1]: http://blog.csdn.net/turkeyzhou/archive/2009/09/16/4558392.aspx