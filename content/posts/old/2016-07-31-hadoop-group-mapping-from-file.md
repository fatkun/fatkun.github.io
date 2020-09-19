---
title: hadoop组映射从配置文件读取
author: fatkun
type: post
date: 2016-07-31T10:41:41+00:00
url: /2016/07/hadoop-group-mapping-from-file.html
duoshuo_thread_id:
  - 6313437859797795585
wp-syntax-cache-content:
  - |
    a:3:{i:1;s:22261:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">package</span> <span style="color: #006699;">cn.uc.hadoop.security</span><span style="color: #339933;">;</span>
    &nbsp;
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.commons.logging.Log</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.commons.logging.LogFactory</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.hadoop.security.GroupMappingServiceProvider</span><span style="color: #339933;">;</span>
    &nbsp;
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">java.io.BufferedReader</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">java.io.FileReader</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">java.io.IOException</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">java.util.ArrayList</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">java.util.HashSet</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">java.util.List</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">java.util.Set</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">java.util.concurrent.ConcurrentHashMap</span><span style="color: #339933;">;</span>
    &nbsp;
    <span style="color: #008000; font-style: italic; font-weight: bold;">/**
     * Created by fatkun on 2016/7/31.
     */</span>
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">class</span> FileBasedUnixGroupsMapping <span style="color: #000000; font-weight: bold;">implements</span> GroupMappingServiceProvider <span style="color: #009900;">&#123;</span>
        <span style="color: #000000; font-weight: bold;">private</span> ConcurrentHashMap<span style="color: #339933;">&lt;</span><span style="color: #003399;">String</span>, List<span style="color: #339933;">&lt;</span>String<span style="color: #339933;">&gt;&gt;</span> groups <span style="color: #339933;">=</span> <span style="color: #000066; font-weight: bold;">null</span><span style="color: #339933;">;</span>
        <span style="color: #000000; font-weight: bold;">private</span> <span style="color: #000000; font-weight: bold;">static</span> <span style="color: #000000; font-weight: bold;">final</span> Log LOG <span style="color: #339933;">=</span> LogFactory.<span style="color: #006633;">getLog</span><span style="color: #009900;">&#40;</span>FileBasedUnixGroupsMapping.<span style="color: #000000; font-weight: bold;">class</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #000000; font-weight: bold;">private</span> <span style="color: #003399;">String</span> confFilePath <span style="color: #339933;">=</span> <span style="color: #0000ff;">&quot;/home/cloudera/var/group/groups.txt&quot;</span><span style="color: #339933;">;</span>
        <span style="color: #666666; font-style: italic;">// 格式： user1=group1,group2</span>
    &nbsp;
        <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">void</span> setConfFilePath<span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span> confFilePath<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            <span style="color: #000000; font-weight: bold;">this</span>.<span style="color: #006633;">confFilePath</span> <span style="color: #339933;">=</span> confFilePath<span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
    &nbsp;
        <span style="color: #000000; font-weight: bold;">private</span> <span style="color: #000000; font-weight: bold;">synchronized</span> <span style="color: #000066; font-weight: bold;">void</span> loadConf<span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">boolean</span> refresh<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    &nbsp;
            <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>refresh <span style="color: #339933;">||</span> groups <span style="color: #339933;">==</span> <span style="color: #000066; font-weight: bold;">null</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
                ConcurrentHashMap<span style="color: #339933;">&lt;</span><span style="color: #003399;">String</span>, List<span style="color: #339933;">&lt;</span>String<span style="color: #339933;">&gt;&gt;</span> tmpGroups <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> ConcurrentHashMap<span style="color: #339933;">&lt;&gt;</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
                <span style="color: #000000; font-weight: bold;">try</span> <span style="color: #009900;">&#123;</span>
                    <span style="color: #003399;">BufferedReader</span> reader <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> <span style="color: #003399;">BufferedReader</span><span style="color: #009900;">&#40;</span><span style="color: #000000; font-weight: bold;">new</span> <span style="color: #003399;">FileReader</span><span style="color: #009900;">&#40;</span>confFilePath<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                    <span style="color: #003399;">String</span> line <span style="color: #339933;">=</span> <span style="color: #000066; font-weight: bold;">null</span><span style="color: #339933;">;</span>
                    <span style="color: #000000; font-weight: bold;">while</span> <span style="color: #009900;">&#40;</span><span style="color: #009900;">&#40;</span>line <span style="color: #339933;">=</span> reader.<span style="color: #006633;">readLine</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">!=</span> <span style="color: #000066; font-weight: bold;">null</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
                        line <span style="color: #339933;">=</span> line.<span style="color: #006633;">trim</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                        <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>line.<span style="color: #006633;">startsWith</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;#&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #000000; font-weight: bold;">continue</span><span style="color: #339933;">;</span>
                        <span style="color: #003399;">String</span><span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span> ugArray <span style="color: #339933;">=</span> line.<span style="color: #006633;">split</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;=&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                        <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>ugArray.<span style="color: #006633;">length</span> <span style="color: #339933;">==</span> <span style="color: #cc66cc;">2</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
                            <span style="color: #003399;">String</span> user <span style="color: #339933;">=</span> ugArray<span style="color: #009900;">&#91;</span><span style="color: #cc66cc;">0</span><span style="color: #009900;">&#93;</span>.<span style="color: #006633;">trim</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                            List<span style="color: #339933;">&lt;</span>String<span style="color: #339933;">&gt;</span> groupList <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> ArrayList<span style="color: #339933;">&lt;&gt;</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                            Set<span style="color: #339933;">&lt;</span>String<span style="color: #339933;">&gt;</span> groupSet <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> HashSet<span style="color: #339933;">&lt;</span>String<span style="color: #339933;">&gt;</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                            groupSet.<span style="color: #006633;">add</span><span style="color: #009900;">&#40;</span>user<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                            <span style="color: #000000; font-weight: bold;">for</span> <span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span> group <span style="color: #339933;">:</span> ugArray<span style="color: #009900;">&#91;</span><span style="color: #cc66cc;">1</span><span style="color: #009900;">&#93;</span>.<span style="color: #006633;">split</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;,&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
                                groupSet.<span style="color: #006633;">add</span><span style="color: #009900;">&#40;</span>group.<span style="color: #006633;">trim</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                            <span style="color: #009900;">&#125;</span>
                            groupList.<span style="color: #006633;">addAll</span><span style="color: #009900;">&#40;</span>groupSet<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                            LOG.<span style="color: #006633;">info</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;add user=&quot;</span> <span style="color: #339933;">+</span> user <span style="color: #339933;">+</span> <span style="color: #0000ff;">&quot; groups=&quot;</span> <span style="color: #339933;">+</span> groupList<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                            tmpGroups.<span style="color: #006633;">put</span><span style="color: #009900;">&#40;</span>user, groupList<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                        <span style="color: #009900;">&#125;</span>
                    <span style="color: #009900;">&#125;</span>
                    reader.<span style="color: #006633;">close</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                <span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">catch</span> <span style="color: #009900;">&#40;</span><span style="color: #003399;">IOException</span> e<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
                    LOG.<span style="color: #006633;">error</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;LOAD GROUP MAPPING ERROR&quot;</span>, e<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                <span style="color: #009900;">&#125;</span>
                groups <span style="color: #339933;">=</span> tmpGroups<span style="color: #339933;">;</span>
            <span style="color: #009900;">&#125;</span>
        <span style="color: #009900;">&#125;</span>
    &nbsp;
        @Override
        <span style="color: #000000; font-weight: bold;">public</span> List<span style="color: #339933;">&lt;</span>String<span style="color: #339933;">&gt;</span> getGroups<span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span> user<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>groups <span style="color: #339933;">==</span> <span style="color: #000066; font-weight: bold;">null</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
                loadConf<span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">false</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #009900;">&#125;</span>
    &nbsp;
            List<span style="color: #339933;">&lt;</span>String<span style="color: #339933;">&gt;</span> groupList <span style="color: #339933;">=</span> groups.<span style="color: #006633;">get</span><span style="color: #009900;">&#40;</span>user<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
            <span style="color: #666666; font-style: italic;">// 如果找不到组配置，返回一个和用户名一样的组名称</span>
            <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>groupList <span style="color: #339933;">==</span> <span style="color: #000066; font-weight: bold;">null</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
                groupList <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> ArrayList<span style="color: #339933;">&lt;&gt;</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                groupList.<span style="color: #006633;">add</span><span style="color: #009900;">&#40;</span>user<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                LOG.<span style="color: #006633;">error</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;CAN'T NOT FIND GROUPS FOR USER &quot;</span> <span style="color: #339933;">+</span> user<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #009900;">&#125;</span>
    &nbsp;
            <span style="color: #000000; font-weight: bold;">return</span> groupList<span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
    &nbsp;
        @Override
        <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">void</span> cacheGroupsRefresh<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            loadConf<span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">true</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
    &nbsp;
        @Override
        <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">void</span> cacheGroupsAdd<span style="color: #009900;">&#40;</span>List<span style="color: #339933;">&lt;</span>String<span style="color: #339933;">&gt;</span> groups<span style="color: #009900;">&#41;</span> <span style="color: #000000; font-weight: bold;">throws</span> <span style="color: #003399;">IOException</span> <span style="color: #009900;">&#123;</span>
            <span style="color: #666666; font-style: italic;">// does nothing in this provider of user to groups mapping</span>
        <span style="color: #009900;">&#125;</span>
    &nbsp;
        <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">static</span> <span style="color: #000066; font-weight: bold;">void</span> main<span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span><span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span> args<span style="color: #009900;">&#41;</span> <span style="color: #000000; font-weight: bold;">throws</span> <span style="color: #003399;">IOException</span> <span style="color: #009900;">&#123;</span>
            FileBasedUnixGroupsMapping f <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> FileBasedUnixGroupsMapping<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            f.<span style="color: #006633;">setConfFilePath</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;d:/tmp/groups.txt&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span>f.<span style="color: #006633;">getGroups</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;impala&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
    <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">package cn.uc.hadoop.security;
    
    import org.apache.commons.logging.Log;
    import org.apache.commons.logging.LogFactory;
    import org.apache.hadoop.security.GroupMappingServiceProvider;
    
    import java.io.BufferedReader;
    import java.io.FileReader;
    import java.io.IOException;
    import java.util.ArrayList;
    import java.util.HashSet;
    import java.util.List;
    import java.util.Set;
    import java.util.concurrent.ConcurrentHashMap;
    
    /**
     * Created by fatkun on 2016/7/31.
     */
    public class FileBasedUnixGroupsMapping implements GroupMappingServiceProvider {
        private ConcurrentHashMap&lt;String, List&lt;String&gt;&gt; groups = null;
        private static final Log LOG = LogFactory.getLog(FileBasedUnixGroupsMapping.class);
        private String confFilePath = &quot;/home/cloudera/var/group/groups.txt&quot;;
        // 格式： user1=group1,group2
    
        public void setConfFilePath(String confFilePath) {
            this.confFilePath = confFilePath;
        }
    
        private synchronized void loadConf(boolean refresh) {
    
            if (refresh || groups == null) {
                ConcurrentHashMap&lt;String, List&lt;String&gt;&gt; tmpGroups = new ConcurrentHashMap&lt;&gt;();
    
                try {
                    BufferedReader reader = new BufferedReader(new FileReader(confFilePath));
                    String line = null;
                    while ((line = reader.readLine()) != null) {
                        line = line.trim();
                        if (line.startsWith(&quot;#&quot;)) continue;
                        String[] ugArray = line.split(&quot;=&quot;);
                        if (ugArray.length == 2) {
                            String user = ugArray[0].trim();
                            List&lt;String&gt; groupList = new ArrayList&lt;&gt;();
                            Set&lt;String&gt; groupSet = new HashSet&lt;String&gt;();
                            groupSet.add(user);
                            for (String group : ugArray[1].split(&quot;,&quot;)) {
                                groupSet.add(group.trim());
                            }
                            groupList.addAll(groupSet);
                            LOG.info(&quot;add user=&quot; + user + &quot; groups=&quot; + groupList);
                            tmpGroups.put(user, groupList);
                        }
                    }
                    reader.close();
                } catch (IOException e) {
                    LOG.error(&quot;LOAD GROUP MAPPING ERROR&quot;, e);
                }
                groups = tmpGroups;
            }
        }
    
        @Override
        public List&lt;String&gt; getGroups(String user) {
            if (groups == null) {
                loadConf(false);
            }
    
            List&lt;String&gt; groupList = groups.get(user);
    
            // 如果找不到组配置，返回一个和用户名一样的组名称
            if (groupList == null) {
                groupList = new ArrayList&lt;&gt;();
                groupList.add(user);
                LOG.error(&quot;CAN'T NOT FIND GROUPS FOR USER &quot; + user);
            }
    
            return groupList;
        }
    
        @Override
        public void cacheGroupsRefresh() {
            loadConf(true);
        }
    
        @Override
        public void cacheGroupsAdd(List&lt;String&gt; groups) throws IOException {
            // does nothing in this provider of user to groups mapping
        }
    
        public static void main(String[] args) throws IOException {
            FileBasedUnixGroupsMapping f = new FileBasedUnixGroupsMapping();
            f.setConfFilePath(&quot;d:/tmp/groups.txt&quot;);
            System.out.println(f.getGroups(&quot;impala&quot;));
        }
    }</p></div>
    ";i:2;s:1454:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="xml" style="font-family:monospace;">  <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;property<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;name<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>hadoop.security.group.mapping<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/name<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;value<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>cn.uc.hadoop.security.FileBasedUnixGroupsMapping<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/value<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/property<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre></td></tr></table><p class="theCode" style="display:none;">  &lt;property&gt;
        &lt;name&gt;hadoop.security.group.mapping&lt;/name&gt;
        &lt;value&gt;cn.uc.hadoop.security.FileBasedUnixGroupsMapping&lt;/value&gt;
      &lt;/property&gt;</p></div>
    ";i:3;s:708:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #007800;">HADOOP_CLASSPATH</span>=<span style="color: #007800;">$HADOOP_CLASSPATH</span>:<span style="color: #000000; font-weight: bold;">/</span>home<span style="color: #000000; font-weight: bold;">/</span>cloudera<span style="color: #000000; font-weight: bold;">/</span>var<span style="color: #000000; font-weight: bold;">/</span>group<span style="color: #000000; font-weight: bold;">/</span>hadoopgroup.jar</pre></td></tr></table><p class="theCode" style="display:none;">HADOOP_CLASSPATH=$HADOOP_CLASSPATH:/home/cloudera/var/group/hadoopgroup.jar</p></div>
    ";}
categories:
  - hadoop
tags:
  - hadoop
  - hdfs
  - namenode

---
hadoop实现类似linux系统的文件权限，需要知道某个用户是属于哪个组。系统默认是使用ShellBasedUnixGroupsMapping 类来获取某个用户属于哪个组，实际是调用id命令来获取用户组信息。为了方便管理，也可以自己实现这个类，通过读取文件的方式来获得组信息。只要实现org.apache.hadoop.security.GroupMappingServiceProvider接口即可，具体可以参考ShellBasedUnixGroupsMapping的实现。
&nbsp;
## 代码

<pre escaped="true" lang="java">package cn.uc.hadoop.security;

import org.apache.commons.logging.Log;
import org.apache.commons.logging.LogFactory;
import org.apache.hadoop.security.GroupMappingServiceProvider;

import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;
import java.util.ArrayList;
import java.util.HashSet;
import java.util.List;
import java.util.Set;
import java.util.concurrent.ConcurrentHashMap;

/**
 * Created by fatkun on 2016/7/31.
 */
public class FileBasedUnixGroupsMapping implements GroupMappingServiceProvider {
    private ConcurrentHashMap&lt;String, List&lt;String&gt;&gt; groups = null;
    private static final Log LOG = LogFactory.getLog(FileBasedUnixGroupsMapping.class);
    private String confFilePath = "/home/cloudera/var/group/groups.txt";
    // 格式： user1=group1,group2

    public void setConfFilePath(String confFilePath) {
        this.confFilePath = confFilePath;
    }

    private synchronized void loadConf(boolean refresh) {

        if (refresh || groups == null) {
            ConcurrentHashMap&lt;String, List&lt;String&gt;&gt; tmpGroups = new ConcurrentHashMap&lt;&gt;();

            try {
                BufferedReader reader = new BufferedReader(new FileReader(confFilePath));
                String line = null;
                while ((line = reader.readLine()) != null) {
                    line = line.trim();
                    if (line.startsWith("#")) continue;
                    String[] ugArray = line.split("=");
                    if (ugArray.length == 2) {
                        String user = ugArray[0].trim();
                        List&lt;String&gt; groupList = new ArrayList&lt;&gt;();
                        Set&lt;String&gt; groupSet = new HashSet&lt;String&gt;();
                        groupSet.add(user);
                        for (String group : ugArray[1].split(",")) {
                            groupSet.add(group.trim());
                        }
                        groupList.addAll(groupSet);
                        LOG.info("add user=" + user + " groups=" + groupList);
                        tmpGroups.put(user, groupList);
                    }
                }
                reader.close();
            } catch (IOException e) {
                LOG.error("LOAD GROUP MAPPING ERROR", e);
            }
            groups = tmpGroups;
        }
    }

    @Override
    public List&lt;String&gt; getGroups(String user) {
        if (groups == null) {
            loadConf(false);
        }

        List&lt;String&gt; groupList = groups.get(user);

        // 如果找不到组配置，返回一个和用户名一样的组名称
        if (groupList == null) {
            groupList = new ArrayList&lt;&gt;();
            groupList.add(user);
            LOG.error("CAN'T NOT FIND GROUPS FOR USER " + user);
        }

        return groupList;
    }

    @Override
    public void cacheGroupsRefresh() {
        loadConf(true);
    }

    @Override
    public void cacheGroupsAdd(List&lt;String&gt; groups) throws IOException {
        // does nothing in this provider of user to groups mapping
    }

    public static void main(String[] args) throws IOException {
        FileBasedUnixGroupsMapping f = new FileBasedUnixGroupsMapping();
        f.setConfFilePath("d:/tmp/groups.txt");
        System.out.println(f.getGroups("impala"));
    }
}</pre>
&nbsp;
## 在cloudera如何使用

在namenode的配置“hdfs-site.xml 的 NameNode 高级配置代码段”加入以下配置，注意不要改“服务级别的hadoop.security.group.mapping”，我们只打算改掉namenode获取组映射的方式
<pre escaped="true" lang="xml">&lt;property&gt;
    &lt;name&gt;hadoop.security.group.mapping&lt;/name&gt;
    &lt;value&gt;cn.uc.hadoop.security.FileBasedUnixGroupsMapping&lt;/value&gt;
  &lt;/property&gt;</pre>
在 “NameNode 环境高级配置代码段（安全阀）”加入（把jar加入namenode的classpath里面）
<pre escaped="true" lang="bash">HADOOP_CLASSPATH=$HADOOP_CLASSPATH:/home/cloudera/var/group/hadoopgroup.jar</pre>
生成groups.txt见 <a href="http://fatkun.com/2016/08/get-user-group-mapping.html" target="_blank">http://fatkun.com/2016/08/get-user-group-mapping.html</a>