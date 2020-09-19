---
title: hadoop job -kill 和 yarn application -kill 区别
author: fatkun
type: post
date: 2017-01-06T10:49:51+00:00
url: /2017/01/hadoop-job-kill-and-yarn-application-kill-diff.html
duoshuo_thread_id:
  - 6372424757081539329
wp-syntax-cache-content:
  - |
    a:4:{i:1;s:9792:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">  @Override
      <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">void</span> killJob<span style="color: #009900;">&#40;</span>JobID arg0<span style="color: #009900;">&#41;</span> <span style="color: #000000; font-weight: bold;">throws</span> <span style="color: #003399;">IOException</span>, <span style="color: #003399;">InterruptedException</span> <span style="color: #009900;">&#123;</span>
        <span style="color: #666666; font-style: italic;">/* check if the status is not running, if not send kill to RM */</span>
        JobStatus status <span style="color: #339933;">=</span> clientCache.<span style="color: #006633;">getClient</span><span style="color: #009900;">&#40;</span>arg0<span style="color: #009900;">&#41;</span>.<span style="color: #006633;">getJobStatus</span><span style="color: #009900;">&#40;</span>arg0<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        ApplicationId appId <span style="color: #339933;">=</span> TypeConverter.<span style="color: #006633;">toYarn</span><span style="color: #009900;">&#40;</span>arg0<span style="color: #009900;">&#41;</span>.<span style="color: #006633;">getAppId</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
        <span style="color: #666666; font-style: italic;">// get status from RM and return</span>
        <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>status <span style="color: #339933;">==</span> <span style="color: #000066; font-weight: bold;">null</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
          killUnFinishedApplication<span style="color: #009900;">&#40;</span>appId<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          <span style="color: #000000; font-weight: bold;">return</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
    &nbsp;
        <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>status.<span style="color: #006633;">getState</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">!=</span> JobStatus.<span style="color: #006633;">State</span>.<span style="color: #006633;">RUNNING</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
          killApplication<span style="color: #009900;">&#40;</span>appId<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          <span style="color: #000000; font-weight: bold;">return</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
    &nbsp;
        <span style="color: #000000; font-weight: bold;">try</span> <span style="color: #009900;">&#123;</span>
          <span style="color: #666666; font-style: italic;">/* send a kill to the AM */</span>
          clientCache.<span style="color: #006633;">getClient</span><span style="color: #009900;">&#40;</span>arg0<span style="color: #009900;">&#41;</span>.<span style="color: #006633;">killJob</span><span style="color: #009900;">&#40;</span>arg0<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          <span style="color: #000066; font-weight: bold;">long</span> currentTimeMillis <span style="color: #339933;">=</span> <span style="color: #003399;">System</span>.<span style="color: #006633;">currentTimeMillis</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          <span style="color: #000066; font-weight: bold;">long</span> timeKillIssued <span style="color: #339933;">=</span> currentTimeMillis<span style="color: #339933;">;</span>
          <span style="color: #000000; font-weight: bold;">while</span> <span style="color: #009900;">&#40;</span><span style="color: #009900;">&#40;</span>currentTimeMillis <span style="color: #339933;">&lt;</span> timeKillIssued <span style="color: #339933;">+</span> 10000L<span style="color: #009900;">&#41;</span>
              <span style="color: #339933;">&amp;&amp;</span> <span style="color: #339933;">!</span>isJobInTerminalState<span style="color: #009900;">&#40;</span>status<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            <span style="color: #000000; font-weight: bold;">try</span> <span style="color: #009900;">&#123;</span>
              <span style="color: #003399;">Thread</span>.<span style="color: #006633;">sleep</span><span style="color: #009900;">&#40;</span>1000L<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">catch</span> <span style="color: #009900;">&#40;</span><span style="color: #003399;">InterruptedException</span> ie<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
              <span style="color: #008000; font-style: italic; font-weight: bold;">/** interrupted, just break */</span>
              <span style="color: #000000; font-weight: bold;">break</span><span style="color: #339933;">;</span>
            <span style="color: #009900;">&#125;</span>
            currentTimeMillis <span style="color: #339933;">=</span> <span style="color: #003399;">System</span>.<span style="color: #006633;">currentTimeMillis</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            status <span style="color: #339933;">=</span> clientCache.<span style="color: #006633;">getClient</span><span style="color: #009900;">&#40;</span>arg0<span style="color: #009900;">&#41;</span>.<span style="color: #006633;">getJobStatus</span><span style="color: #009900;">&#40;</span>arg0<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>status <span style="color: #339933;">==</span> <span style="color: #000066; font-weight: bold;">null</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
              killUnFinishedApplication<span style="color: #009900;">&#40;</span>appId<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
              <span style="color: #000000; font-weight: bold;">return</span><span style="color: #339933;">;</span>
            <span style="color: #009900;">&#125;</span>
          <span style="color: #009900;">&#125;</span>
        <span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">catch</span><span style="color: #009900;">&#40;</span><span style="color: #003399;">IOException</span> io<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
          LOG.<span style="color: #006633;">debug</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;Error when checking for application status&quot;</span>, io<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
        <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>status <span style="color: #339933;">!=</span> <span style="color: #000066; font-weight: bold;">null</span> <span style="color: #339933;">&amp;&amp;</span> <span style="color: #339933;">!</span>isJobInTerminalState<span style="color: #009900;">&#40;</span>status<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
          killApplication<span style="color: #009900;">&#40;</span>appId<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
      <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">  @Override
      public void killJob(JobID arg0) throws IOException, InterruptedException {
        /* check if the status is not running, if not send kill to RM */
        JobStatus status = clientCache.getClient(arg0).getJobStatus(arg0);
        ApplicationId appId = TypeConverter.toYarn(arg0).getAppId();
    
        // get status from RM and return
        if (status == null) {
          killUnFinishedApplication(appId);
          return;
        }
    
        if (status.getState() != JobStatus.State.RUNNING) {
          killApplication(appId);
          return;
        }
    
        try {
          /* send a kill to the AM */
          clientCache.getClient(arg0).killJob(arg0);
          long currentTimeMillis = System.currentTimeMillis();
          long timeKillIssued = currentTimeMillis;
          while ((currentTimeMillis &lt; timeKillIssued + 10000L)
              &amp;&amp; !isJobInTerminalState(status)) {
            try {
              Thread.sleep(1000L);
            } catch (InterruptedException ie) {
              /** interrupted, just break */
              break;
            }
            currentTimeMillis = System.currentTimeMillis();
            status = clientCache.getClient(arg0).getJobStatus(arg0);
            if (status == null) {
              killUnFinishedApplication(appId);
              return;
            }
          }
        } catch(IOException io) {
          LOG.debug(&quot;Error when checking for application status&quot;, io);
        }
        if (status != null &amp;&amp; !isJobInTerminalState(status)) {
          killApplication(appId);
        }
      }</p></div>
    ";i:2;s:4716:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">    @SuppressWarnings<span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;unchecked&quot;</span><span style="color: #009900;">&#41;</span>
        @Override
        <span style="color: #000000; font-weight: bold;">public</span> KillJobResponse killJob<span style="color: #009900;">&#40;</span>KillJobRequest request<span style="color: #009900;">&#41;</span> 
          <span style="color: #000000; font-weight: bold;">throws</span> <span style="color: #003399;">IOException</span> <span style="color: #009900;">&#123;</span>
          JobId jobId <span style="color: #339933;">=</span> request.<span style="color: #006633;">getJobId</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          UserGroupInformation callerUGI <span style="color: #339933;">=</span> UserGroupInformation.<span style="color: #006633;">getCurrentUser</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          <span style="color: #003399;">String</span> message <span style="color: #339933;">=</span> <span style="color: #0000ff;">&quot;Kill job &quot;</span> <span style="color: #339933;">+</span> jobId <span style="color: #339933;">+</span> <span style="color: #0000ff;">&quot; received from &quot;</span> <span style="color: #339933;">+</span> callerUGI
              <span style="color: #339933;">+</span> <span style="color: #0000ff;">&quot; at &quot;</span> <span style="color: #339933;">+</span> Server.<span style="color: #006633;">getRemoteAddress</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          LOG.<span style="color: #006633;">info</span><span style="color: #009900;">&#40;</span>message<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          verifyAndGetJob<span style="color: #009900;">&#40;</span>jobId, JobACL.<span style="color: #006633;">MODIFY_JOB</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          appContext.<span style="color: #006633;">getEventHandler</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">handle</span><span style="color: #009900;">&#40;</span>
              <span style="color: #000000; font-weight: bold;">new</span> JobDiagnosticsUpdateEvent<span style="color: #009900;">&#40;</span>jobId, message<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          appContext.<span style="color: #006633;">getEventHandler</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">handle</span><span style="color: #009900;">&#40;</span>
              <span style="color: #000000; font-weight: bold;">new</span> JobEvent<span style="color: #009900;">&#40;</span>jobId, JobEventType.<span style="color: #006633;">JOB_KILL</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          KillJobResponse response <span style="color: #339933;">=</span> 
            recordFactory.<span style="color: #006633;">newRecordInstance</span><span style="color: #009900;">&#40;</span>KillJobResponse.<span style="color: #000000; font-weight: bold;">class</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          <span style="color: #000000; font-weight: bold;">return</span> response<span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">    @SuppressWarnings(&quot;unchecked&quot;)
        @Override
        public KillJobResponse killJob(KillJobRequest request) 
          throws IOException {
          JobId jobId = request.getJobId();
          UserGroupInformation callerUGI = UserGroupInformation.getCurrentUser();
          String message = &quot;Kill job &quot; + jobId + &quot; received from &quot; + callerUGI
              + &quot; at &quot; + Server.getRemoteAddress();
          LOG.info(message);
          verifyAndGetJob(jobId, JobACL.MODIFY_JOB);
          appContext.getEventHandler().handle(
              new JobDiagnosticsUpdateEvent(jobId, message));
          appContext.getEventHandler().handle(
              new JobEvent(jobId, JobEventType.JOB_KILL));
          KillJobResponse response = 
            recordFactory.newRecordInstance(KillJobResponse.class);
          return response;
        }</p></div>
    ";i:3;s:5869:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #008000; font-style: italic; font-weight: bold;">/**
       * Kills the application with the application id as appId
       * 
       * @param applicationId
       * @throws YarnException
       * @throws IOException
       */</span>
      <span style="color: #000000; font-weight: bold;">private</span> <span style="color: #000066; font-weight: bold;">void</span> killApplication<span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span> applicationId<span style="color: #009900;">&#41;</span> <span style="color: #000000; font-weight: bold;">throws</span> YarnException,
          <span style="color: #003399;">IOException</span> <span style="color: #009900;">&#123;</span>
        ApplicationId appId <span style="color: #339933;">=</span> ConverterUtils.<span style="color: #006633;">toApplicationId</span><span style="color: #009900;">&#40;</span>applicationId<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        ApplicationReport  appReport <span style="color: #339933;">=</span> <span style="color: #000066; font-weight: bold;">null</span><span style="color: #339933;">;</span>
        <span style="color: #000000; font-weight: bold;">try</span> <span style="color: #009900;">&#123;</span>
          appReport <span style="color: #339933;">=</span> client.<span style="color: #006633;">getApplicationReport</span><span style="color: #009900;">&#40;</span>appId<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">catch</span> <span style="color: #009900;">&#40;</span>ApplicationNotFoundException e<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
          sysout.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;Application with id '&quot;</span> <span style="color: #339933;">+</span> applicationId <span style="color: #339933;">+</span>
              <span style="color: #0000ff;">&quot;' doesn't exist in RM.&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          <span style="color: #000000; font-weight: bold;">throw</span> e<span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
    &nbsp;
        <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>appReport.<span style="color: #006633;">getYarnApplicationState</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">==</span> YarnApplicationState.<span style="color: #006633;">FINISHED</span>
            <span style="color: #339933;">||</span> appReport.<span style="color: #006633;">getYarnApplicationState</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">==</span> YarnApplicationState.<span style="color: #006633;">KILLED</span>
            <span style="color: #339933;">||</span> appReport.<span style="color: #006633;">getYarnApplicationState</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">==</span> YarnApplicationState.<span style="color: #006633;">FAILED</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
          sysout.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;Application &quot;</span> <span style="color: #339933;">+</span> applicationId <span style="color: #339933;">+</span> <span style="color: #0000ff;">&quot; has already finished &quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">else</span> <span style="color: #009900;">&#123;</span>
          sysout.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;Killing application &quot;</span> <span style="color: #339933;">+</span> applicationId<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          client.<span style="color: #006633;">killApplication</span><span style="color: #009900;">&#40;</span>appId<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
      <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">/**
       * Kills the application with the application id as appId
       * 
       * @param applicationId
       * @throws YarnException
       * @throws IOException
       */
      private void killApplication(String applicationId) throws YarnException,
          IOException {
        ApplicationId appId = ConverterUtils.toApplicationId(applicationId);
        ApplicationReport  appReport = null;
        try {
          appReport = client.getApplicationReport(appId);
        } catch (ApplicationNotFoundException e) {
          sysout.println(&quot;Application with id '&quot; + applicationId +
              &quot;' doesn't exist in RM.&quot;);
          throw e;
        }
    
        if (appReport.getYarnApplicationState() == YarnApplicationState.FINISHED
            || appReport.getYarnApplicationState() == YarnApplicationState.KILLED
            || appReport.getYarnApplicationState() == YarnApplicationState.FAILED) {
          sysout.println(&quot;Application &quot; + applicationId + &quot; has already finished &quot;);
        } else {
          sysout.println(&quot;Killing application &quot; + applicationId);
          client.killApplication(appId);
        }
      }</p></div>
    ";i:4;s:8051:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">  @Override
      <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">void</span> killApplication<span style="color: #009900;">&#40;</span>ApplicationId applicationId<span style="color: #009900;">&#41;</span>
          <span style="color: #000000; font-weight: bold;">throws</span> YarnException, <span style="color: #003399;">IOException</span> <span style="color: #009900;">&#123;</span>
        KillApplicationRequest request <span style="color: #339933;">=</span>
            Records.<span style="color: #006633;">newRecord</span><span style="color: #009900;">&#40;</span>KillApplicationRequest.<span style="color: #000000; font-weight: bold;">class</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        request.<span style="color: #006633;">setApplicationId</span><span style="color: #009900;">&#40;</span>applicationId<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
        <span style="color: #000000; font-weight: bold;">try</span> <span style="color: #009900;">&#123;</span>
          <span style="color: #000066; font-weight: bold;">int</span> pollCount <span style="color: #339933;">=</span> <span style="color: #cc66cc;">0</span><span style="color: #339933;">;</span>
          <span style="color: #000066; font-weight: bold;">long</span> startTime <span style="color: #339933;">=</span> <span style="color: #003399;">System</span>.<span style="color: #006633;">currentTimeMillis</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
          <span style="color: #000000; font-weight: bold;">while</span> <span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">true</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            KillApplicationResponse response <span style="color: #339933;">=</span>
                rmClient.<span style="color: #006633;">forceKillApplication</span><span style="color: #009900;">&#40;</span>request<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>response.<span style="color: #006633;">getIsKillCompleted</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
              LOG.<span style="color: #006633;">info</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;Killed application &quot;</span> <span style="color: #339933;">+</span> applicationId<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
              <span style="color: #000000; font-weight: bold;">break</span><span style="color: #339933;">;</span>
            <span style="color: #009900;">&#125;</span>
    &nbsp;
            <span style="color: #000066; font-weight: bold;">long</span> elapsedMillis <span style="color: #339933;">=</span> <span style="color: #003399;">System</span>.<span style="color: #006633;">currentTimeMillis</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">-</span> startTime<span style="color: #339933;">;</span>
            <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>enforceAsyncAPITimeout<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">&amp;&amp;</span>
                elapsedMillis <span style="color: #339933;">&gt;=</span> <span style="color: #000000; font-weight: bold;">this</span>.<span style="color: #006633;">asyncApiPollTimeoutMillis</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
              <span style="color: #000000; font-weight: bold;">throw</span> <span style="color: #000000; font-weight: bold;">new</span> YarnException<span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;Timed out while waiting for application &quot;</span> <span style="color: #339933;">+</span>
                applicationId <span style="color: #339933;">+</span> <span style="color: #0000ff;">&quot; to be killed.&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #009900;">&#125;</span>
    &nbsp;
            <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span><span style="color: #339933;">++</span>pollCount <span style="color: #339933;">%</span> <span style="color: #cc66cc;">10</span> <span style="color: #339933;">==</span> <span style="color: #cc66cc;">0</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
              LOG.<span style="color: #006633;">info</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;Waiting for application &quot;</span> <span style="color: #339933;">+</span> applicationId <span style="color: #339933;">+</span> <span style="color: #0000ff;">&quot; to be killed.&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #009900;">&#125;</span>
            <span style="color: #003399;">Thread</span>.<span style="color: #006633;">sleep</span><span style="color: #009900;">&#40;</span>asyncApiPollIntervalMillis<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          <span style="color: #009900;">&#125;</span>
        <span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">catch</span> <span style="color: #009900;">&#40;</span><span style="color: #003399;">InterruptedException</span> e<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
          LOG.<span style="color: #006633;">error</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;Interrupted while waiting for application &quot;</span> <span style="color: #339933;">+</span> applicationId
              <span style="color: #339933;">+</span> <span style="color: #0000ff;">&quot; to be killed.&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
      <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">  @Override
      public void killApplication(ApplicationId applicationId)
          throws YarnException, IOException {
        KillApplicationRequest request =
            Records.newRecord(KillApplicationRequest.class);
        request.setApplicationId(applicationId);
    
        try {
          int pollCount = 0;
          long startTime = System.currentTimeMillis();
    
          while (true) {
            KillApplicationResponse response =
                rmClient.forceKillApplication(request);
            if (response.getIsKillCompleted()) {
              LOG.info(&quot;Killed application &quot; + applicationId);
              break;
            }
    
            long elapsedMillis = System.currentTimeMillis() - startTime;
            if (enforceAsyncAPITimeout() &amp;&amp;
                elapsedMillis &gt;= this.asyncApiPollTimeoutMillis) {
              throw new YarnException(&quot;Timed out while waiting for application &quot; +
                applicationId + &quot; to be killed.&quot;);
            }
    
            if (++pollCount % 10 == 0) {
              LOG.info(&quot;Waiting for application &quot; + applicationId + &quot; to be killed.&quot;);
            }
            Thread.sleep(asyncApiPollIntervalMillis);
          }
        } catch (InterruptedException e) {
          LOG.error(&quot;Interrupted while waiting for application &quot; + applicationId
              + &quot; to be killed.&quot;);
        }
      }</p></div>
    ";}
categories:
  - hadoop

---
hadoop job -kill 调用的是CLI.java里面的job.killJob(); 这里会分几种情况，如果是能查询到状态是RUNNING的话，是直接向AppMaster发送kill请求的。  
YARNRunner.java 
<pre escaped="true" lang="java">@Override
  public void killJob(JobID arg0) throws IOException, InterruptedException {
    /* check if the status is not running, if not send kill to RM */
    JobStatus status = clientCache.getClient(arg0).getJobStatus(arg0);
    ApplicationId appId = TypeConverter.toYarn(arg0).getAppId();

    // get status from RM and return
    if (status == null) {
      killUnFinishedApplication(appId);
      return;
    }

    if (status.getState() != JobStatus.State.RUNNING) {
      killApplication(appId);
      return;
    }

    try {
      /* send a kill to the AM */
      clientCache.getClient(arg0).killJob(arg0);
      long currentTimeMillis = System.currentTimeMillis();
      long timeKillIssued = currentTimeMillis;
      while ((currentTimeMillis &lt; timeKillIssued + 10000L)
          && !isJobInTerminalState(status)) {
        try {
          Thread.sleep(1000L);
        } catch (InterruptedException ie) {
          /** interrupted, just break */
          break;
        }
        currentTimeMillis = System.currentTimeMillis();
        status = clientCache.getClient(arg0).getJobStatus(arg0);
        if (status == null) {
          killUnFinishedApplication(appId);
          return;
        }
      }
    } catch(IOException io) {
      LOG.debug("Error when checking for application status", io);
    }
    if (status != null && !isJobInTerminalState(status)) {
      killApplication(appId);
    }
  }</pre>
MRClientService.java
<pre escaped="true" lang="java">@SuppressWarnings("unchecked")
    @Override
    public KillJobResponse killJob(KillJobRequest request) 
      throws IOException {
      JobId jobId = request.getJobId();
      UserGroupInformation callerUGI = UserGroupInformation.getCurrentUser();
      String message = "Kill job " + jobId + " received from " + callerUGI
          + " at " + Server.getRemoteAddress();
      LOG.info(message);
      verifyAndGetJob(jobId, JobACL.MODIFY_JOB);
      appContext.getEventHandler().handle(
          new JobDiagnosticsUpdateEvent(jobId, message));
      appContext.getEventHandler().handle(
          new JobEvent(jobId, JobEventType.JOB_KILL));
      KillJobResponse response = 
        recordFactory.newRecordInstance(KillJobResponse.class);
      return response;
    }</pre>
yarn application -kill 使用的是ApplicationCLI.java，是向RM发送kill请求
<pre escaped="true" lang="java">/**
   * Kills the application with the application id as appId
   * 
   * @param applicationId
   * @throws YarnException
   * @throws IOException
   */
  private void killApplication(String applicationId) throws YarnException,
      IOException {
    ApplicationId appId = ConverterUtils.toApplicationId(applicationId);
    ApplicationReport  appReport = null;
    try {
      appReport = client.getApplicationReport(appId);
    } catch (ApplicationNotFoundException e) {
      sysout.println("Application with id '" + applicationId +
          "' doesn't exist in RM.");
      throw e;
    }

    if (appReport.getYarnApplicationState() == YarnApplicationState.FINISHED
        || appReport.getYarnApplicationState() == YarnApplicationState.KILLED
        || appReport.getYarnApplicationState() == YarnApplicationState.FAILED) {
      sysout.println("Application " + applicationId + " has already finished ");
    } else {
      sysout.println("Killing application " + applicationId);
      client.killApplication(appId);
    }
  }</pre>
YarnClientImpl.java
<pre escaped="true" lang="java">@Override
  public void killApplication(ApplicationId applicationId)
      throws YarnException, IOException {
    KillApplicationRequest request =
        Records.newRecord(KillApplicationRequest.class);
    request.setApplicationId(applicationId);

    try {
      int pollCount = 0;
      long startTime = System.currentTimeMillis();

      while (true) {
        KillApplicationResponse response =
            rmClient.forceKillApplication(request);
        if (response.getIsKillCompleted()) {
          LOG.info("Killed application " + applicationId);
          break;
        }

        long elapsedMillis = System.currentTimeMillis() - startTime;
        if (enforceAsyncAPITimeout() &&
            elapsedMillis &gt;= this.asyncApiPollTimeoutMillis) {
          throw new YarnException("Timed out while waiting for application " +
            applicationId + " to be killed.");
        }

        if (++pollCount % 10 == 0) {
          LOG.info("Waiting for application " + applicationId + " to be killed.");
        }
        Thread.sleep(asyncApiPollIntervalMillis);
      }
    } catch (InterruptedException e) {
      LOG.error("Interrupted while waiting for application " + applicationId
          + " to be killed.");
    }
  }</pre>