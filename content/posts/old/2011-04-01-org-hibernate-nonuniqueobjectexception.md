---
title: org.hibernate.NonUniqueObjectException的原因与解决方法
author: fatkun
type: post
date: 2011-04-01T09:42:12+00:00
url: /2011/04/org-hibernate-nonuniqueobjectexception.html
duoshuo_thread_id:
  - 6300408803498132226
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:1664:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">User user1 <span style="color: #339933;">=</span> session.<span style="color: #006633;">load</span><span style="color: #009900;">&#40;</span><span style="color: #cc66cc;">1</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    User user2 <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> User<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    user2.<span style="color: #006633;">setId</span><span style="color: #009900;">&#40;</span><span style="color: #cc66cc;">1</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span><span style="color: #666666; font-style: italic;">//此时ID和user1一样</span>
    user2.<span style="color: #006633;">setUsername</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;fatkun&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    session.<span style="color: #006633;">update</span><span style="color: #009900;">&#40;</span>user2<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span><span style="color: #666666; font-style: italic;">//这里会抛出错误</span></pre></td></tr></table><p class="theCode" style="display:none;">User user1 = session.load(1);
    User user2 = new User();
    user2.setId(1);//此时ID和user1一样
    user2.setUsername(&quot;fatkun&quot;);
    session.update(user2);//这里会抛出错误</p></div>
    ";}
categories:
  - J2EE
tags:
  - hibernate
  - NonUniqueObjectException

---
使用hibernate更新对象时，出现如下错误：  
org.hibernate.NonUniqueObjectException: a different object with the same identifier value was already associated with the session:[com.fatkun.dao.hibernate.User#12]
## 原因

在同一个session内，如果已经有一个对象已经是持久化状态(load进来等)，现在构造一个新的PO，和前一个持久化对象拥有相同的持久化标识(identifier)，在update的时候，就会抛这个错误。  
举个例子（伪代码）：
<pre escaped="true" lang="java">User user1 = session.load(1);
User user2 = new User();
user2.setId(1);//此时ID和user1一样
user2.setUsername("fatkun");
session.update(user2);//这里会抛出错误</pre>
## 解决方法

1.不要重新new一个对象，使用load的对象对他进行更改值。  
例如上面例子直接对user1操作，最后更新user1  
2.如果是hibernate3以上，可以使用session.merge()方法  
3.把session中同标识的对象移出(session.evict(user1))，使他成为脱管的状态，然后user2就可以update了。