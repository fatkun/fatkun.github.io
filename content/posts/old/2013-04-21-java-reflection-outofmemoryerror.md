---
title: 'java反射引起的java.lang.OutOfMemoryError: PermGen space'
author: fatkun
type: post
date: 2013-04-21T13:50:58+00:00
url: /2013/04/java-reflection-outofmemoryerror.html
duoshuo_thread_id:
  - 6300410014842487554
wp-syntax-cache-content:
  - |
    a:2:{i:1;s:5949:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">            Hive hive <span style="color: #339933;">=</span> Hive.<span style="color: #006633;">get</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                <span style="color: #003399;">Method</span> method <span style="color: #339933;">=</span> Hive.<span style="color: #000000; font-weight: bold;">class</span>.<span style="color: #006633;">getDeclaredMethod</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;getMSC&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                method.<span style="color: #006633;">setAccessible</span><span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">true</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                HiveMetaStoreClient msc <span style="color: #339933;">=</span> <span style="color: #009900;">&#40;</span>HiveMetaStoreClient<span style="color: #009900;">&#41;</span>method.<span style="color: #006633;">invoke</span><span style="color: #009900;">&#40;</span>hive<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                <span style="color: #003399;">Field</span> field <span style="color: #339933;">=</span> HiveMetaStoreClient.<span style="color: #000000; font-weight: bold;">class</span>.<span style="color: #006633;">getDeclaredField</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;client&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                field.<span style="color: #006633;">setAccessible</span><span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">true</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                HiveMetaStore.<span style="color: #006633;">HMSHandler</span> client <span style="color: #339933;">=</span> <span style="color: #009900;">&#40;</span>HiveMetaStore.<span style="color: #006633;">HMSHandler</span><span style="color: #009900;">&#41;</span>field.<span style="color: #006633;">get</span><span style="color: #009900;">&#40;</span>msc<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                
                <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>client <span style="color: #339933;">!=</span> <span style="color: #000066; font-weight: bold;">null</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
                    method <span style="color: #339933;">=</span> HiveMetaStore.<span style="color: #006633;">HMSHandler</span>.<span style="color: #000000; font-weight: bold;">class</span>.<span style="color: #006633;">getDeclaredMethod</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;getMS&quot;</span>, <span style="color: #000066; font-weight: bold;">boolean</span>.<span style="color: #000000; font-weight: bold;">class</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                    method.<span style="color: #006633;">setAccessible</span><span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">true</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                    ObjectStore os <span style="color: #339933;">=</span> <span style="color: #009900;">&#40;</span>ObjectStore<span style="color: #009900;">&#41;</span>method.<span style="color: #006633;">invoke</span><span style="color: #009900;">&#40;</span>client, <span style="color: #000066; font-weight: bold;">false</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                    os.<span style="color: #006633;">shutdown</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                <span style="color: #009900;">&#125;</span>
                method <span style="color: #339933;">=</span> <span style="color: #000066; font-weight: bold;">null</span><span style="color: #339933;">;</span>
                field <span style="color: #339933;">=</span> <span style="color: #000066; font-weight: bold;">null</span><span style="color: #339933;">;</span>
                
                Hive.<span style="color: #006633;">closeCurrent</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span></pre></td></tr></table><p class="theCode" style="display:none;">            Hive hive = Hive.get();
                Method method = Hive.class.getDeclaredMethod(&quot;getMSC&quot;);
                method.setAccessible(true);
                HiveMetaStoreClient msc = (HiveMetaStoreClient)method.invoke(hive);
                Field field = HiveMetaStoreClient.class.getDeclaredField(&quot;client&quot;);
                field.setAccessible(true);
                HiveMetaStore.HMSHandler client = (HiveMetaStore.HMSHandler)field.get(msc);
                
                if (client != null) {
                    method = HiveMetaStore.HMSHandler.class.getDeclaredMethod(&quot;getMS&quot;, boolean.class);
                    method.setAccessible(true);
                    ObjectStore os = (ObjectStore)method.invoke(client, false);
                    os.shutdown();
                }
                method = null;
                field = null;
                
                Hive.closeCurrent();</p></div>
    ";i:2;s:457:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #339933;">-</span>Dsun.<span style="color: #006633;">reflect</span>.<span style="color: #006633;">inflationThreshold</span><span style="color: #339933;">=</span><span style="color: #cc66cc;">0</span></pre></td></tr></table><p class="theCode" style="display:none;">-Dsun.reflect.inflationThreshold=0</p></div>
    ";}
categories:
  - J2EE
tags:
  - JAVA
  - OutOfMemoryError
  - reflect

---
由于之前为了不改hive的代码，用了反射的方式动态修改，导致了另一个问题出现。  
我用的反射代码如下：（代码是针对local metastore写的）, 主要是为了调用ObjectStore的shutdown()方法。
<pre escaped="true" lang="java">            Hive hive = Hive.get();
            Method method = Hive.class.getDeclaredMethod("getMSC");
            method.setAccessible(true);
            HiveMetaStoreClient msc = (HiveMetaStoreClient)method.invoke(hive);
            Field field = HiveMetaStoreClient.class.getDeclaredField("client");
            field.setAccessible(true);
            HiveMetaStore.HMSHandler client = (HiveMetaStore.HMSHandler)field.get(msc);
            
            if (client != null) {
                method = HiveMetaStore.HMSHandler.class.getDeclaredMethod("getMS", boolean.class);
                method.setAccessible(true);
                ObjectStore os = (ObjectStore)method.invoke(client, false);
                os.shutdown();
            }
            method = null;
            field = null;
            
            Hive.closeCurrent();</pre>
使用反射后，用jprofiler检查发现多了很多这些类  
sun.reflect.DelegatingClassLoader  
sun.reflect.GeneratedConstructorAccessor77
估计是反射引起的，类越來越多（还没有严谨的测试过，因为perm内存增长很缓慢）  
看了几篇文章，没搞懂。。到<a href="http://stackoverflow.com/questions/16130292/java-lang-outofmemoryerror-permgen-space-java-reflection?answertab=active" target="_blank">StackOverflow</a>去问 
使用这个参数，通过jni的方式调用反射
<pre escaped="true" lang="java">-Dsun.reflect.inflationThreshold=0</pre>
我理解是使用反射会有两种途径，jni和Java bytecode，（It can use a JNI accessor, or a Java bytecode accessor），使用jni调用会慢一些，但使用Java bytecode会生成一个类和classloader (sun/reflect/GeneratedMethodAccessor<N> class and sun/reflect/DelegatingClassLoader)。JVM刚开始默认使用JNI的方式调用，当同一个类调用次数达到一定值后改为Java bytecode调用。
可能会有少许的性能缺失,但我调用的次数还不算多，应该可以接受。另外发现在线上的对象个数有150个左右，应该有些内存还是被回收了，调用的次数不止那么少。
## 参考

<a href="http://stackoverflow.com/questions/16130292/java-lang-outofmemoryerror-permgen-space-java-reflection?answertab=active" target="_blank">StackOverflow</a>  
<a href="http://www-01.ibm.com/support/docview.wss?uid=swg21566549" target="_blank">Potential native memory use in reflection delegating classloaders</a>