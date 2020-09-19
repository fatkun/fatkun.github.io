---
title: 使用MultipleOutputs报File already exists错误
author: fatkun
type: post
date: 2018-08-04T04:21:53+00:00
url: /2018/08/use-multipleoutputs-file-already-exists.html
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:3975:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">  @<span style="color: #000000; font-weight: bold;">Private</span>
      <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">void</span> abortTask<span style="color: #009900;">&#40;</span>TaskAttemptContext context, Path taskAttemptPath<span style="color: #009900;">&#41;</span> <span style="color: #000000; font-weight: bold;">throws</span> <span style="color: #003399;">IOException</span> <span style="color: #009900;">&#123;</span>
        <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>hasOutputPath<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span> 
          context.<span style="color: #006633;">progress</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          <span style="color: #000000; font-weight: bold;">if</span><span style="color: #009900;">&#40;</span>taskAttemptPath <span style="color: #339933;">==</span> <span style="color: #000066; font-weight: bold;">null</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            taskAttemptPath <span style="color: #339933;">=</span> getTaskAttemptPath<span style="color: #009900;">&#40;</span>context<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          <span style="color: #009900;">&#125;</span>
          FileSystem fs <span style="color: #339933;">=</span> taskAttemptPath.<span style="color: #006633;">getFileSystem</span><span style="color: #009900;">&#40;</span>context.<span style="color: #006633;">getConfiguration</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          <span style="color: #000000; font-weight: bold;">if</span><span style="color: #009900;">&#40;</span><span style="color: #339933;">!</span>fs.<span style="color: #006633;">delete</span><span style="color: #009900;">&#40;</span>taskAttemptPath, <span style="color: #000066; font-weight: bold;">true</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            LOG.<span style="color: #006633;">warn</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;Could not delete &quot;</span><span style="color: #339933;">+</span>taskAttemptPath<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          <span style="color: #009900;">&#125;</span>
        <span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">else</span> <span style="color: #009900;">&#123;</span>
          LOG.<span style="color: #006633;">warn</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;Output Path is null in abortTask()&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
      <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">  @Private
      public void abortTask(TaskAttemptContext context, Path taskAttemptPath) throws IOException {
        if (hasOutputPath()) { 
          context.progress();
          if(taskAttemptPath == null) {
            taskAttemptPath = getTaskAttemptPath(context);
          }
          FileSystem fs = taskAttemptPath.getFileSystem(context.getConfiguration());
          if(!fs.delete(taskAttemptPath, true)) {
            LOG.warn(&quot;Could not delete &quot;+taskAttemptPath);
          }
        } else {
          LOG.warn(&quot;Output Path is null in abortTask()&quot;);
        }
      }</p></div>
    ";}
categories:
  - hadoop

---
在reduce任务看到第一个任务因为某些原因失败了，但后续的任务都一起失败，后续的任务报File already exists错误。
原因是MultipleOutputs.write的时候可以指定输出的别名或者绝对路径，如果写的是绝对路径，目录会马上生效，MR的output commit机制会失效（先输出到临时目录，然后最后移动回正式目录）。当任务第一次失败后，第二次重试还是存在着那个文件会报错退出。
MR会在任务失败的时候清理输出，但仅限于taskAttemptPath，不会清理其他产生的文件。
<pre lang="java" escaped="true">@Private
  public void abortTask(TaskAttemptContext context, Path taskAttemptPath) throws IOException {
    if (hasOutputPath()) { 
      context.progress();
      if(taskAttemptPath == null) {
        taskAttemptPath = getTaskAttemptPath(context);
      }
      FileSystem fs = taskAttemptPath.getFileSystem(context.getConfiguration());
      if(!fs.delete(taskAttemptPath, true)) {
        LOG.warn("Could not delete "+taskAttemptPath);
      }
    } else {
      LOG.warn("Output Path is null in abortTask()");
    }
  }</pre>
## 解决方法

想办法在第二次跑之前清理文件。最终输出的文件名是用户指定路径+数字，那个数字不太好从哪里获取到，另外如果开了推测执行，推测执行的任务也会失败。
解决的方法还是不要用绝对路径输出，按key输出文件，最后如果需要分开目录的时候再在client那边把文件移动过去。
&nbsp;
## 相关issue

这个issue只是指出如果用绝对路径，output committing的机制会失效，加了个警告注释  
https://issues.apache.org/jira/browse/MAPREDUCE-6357