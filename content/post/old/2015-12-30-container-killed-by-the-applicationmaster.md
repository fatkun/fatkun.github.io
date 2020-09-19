---
title: Container killed by the ApplicationMaster, Exit code is 143
author: fatkun
type: post
date: 2015-12-30T13:14:03+00:00
url: /2015/12/container-killed-by-the-applicationmaster.html
duoshuo_thread_id:
  - 6300421658352026370
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:7727:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="other" style="font-family:monospace;">2015-12-30 17:31:09,994 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.TaskAttemptImpl: attempt_1451360650431_0228_m_000000_0 TaskAttempt Transitioned from RUNNING to SUCCESS_CONTAINER_CLEANUP
    2015-12-30 17:31:09,995 INFO [ContainerLauncher #1] org.apache.hadoop.mapreduce.v2.app.launcher.ContainerLauncherImpl: Processing the event EventType: CONTAINER_REMOTE_CLEANUP for container container_1451360650431_0228_01_000002 taskAttempt attempt_1451360650431_0228_m_000000_0
    2015-12-30 17:31:09,995 INFO [ContainerLauncher #1] org.apache.hadoop.mapreduce.v2.app.launcher.ContainerLauncherImpl: KILLING attempt_1451360650431_0228_m_000000_0
    2015-12-30 17:31:09,995 INFO [ContainerLauncher #1] org.apache.hadoop.yarn.client.api.impl.ContainerManagementProtocolProxy: Opening proxy : uaerouter2-vm02:8041
    2015-12-30 17:31:10,012 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.TaskAttemptImpl: attempt_1451360650431_0228_m_000000_0 TaskAttempt Transitioned from SUCCESS_CONTAINER_CLEANUP to SUCCEEDED
    2015-12-30 17:31:10,020 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.TaskImpl: Task succeeded with attempt attempt_1451360650431_0228_m_000000_0
    2015-12-30 17:31:10,021 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.TaskImpl: task_1451360650431_0228_m_000000 Task Transitioned from RUNNING to SUCCEEDED
    2015-12-30 17:31:10,023 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.JobImpl: Num completed Tasks: 1
    2015-12-30 17:31:10,895 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Before Scheduling: PendingReds:1 ScheduledMaps:0 ScheduledReds:0 AssignedMaps:1 AssignedReds:0 CompletedMaps:1 CompletedReds:0 ContAlloc:1 ContRel:0 HostLocal:1 RackLocal:0
    2015-12-30 17:31:10,898 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Recalculating schedule, headroom=&lt;memory:14336, vCores:14&gt;
    2015-12-30 17:31:10,898 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Reduce slow start threshold reached. Scheduling reduces.
    2015-12-30 17:31:10,898 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: All maps assigned. Ramping up all remaining reduces:1
    2015-12-30 17:31:10,898 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: After Scheduling: PendingReds:0 ScheduledMaps:0 ScheduledReds:1 AssignedMaps:1 AssignedReds:0 CompletedMaps:1 CompletedReds:0 ContAlloc:1 ContRel:0 HostLocal:1 RackLocal:0
    2015-12-30 17:31:11,906 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerRequestor: getResources() for application_1451360650431_0228: ask=1 release= 0 newContainers=0 finishedContainers=1 resourcelimit=&lt;memory:15360, vCores:15&gt; knownNMs=2
    2015-12-30 17:31:11,906 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Received completed container container_1451360650431_0228_01_000002
    2015-12-30 17:31:11,907 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: After Scheduling: PendingReds:0 ScheduledMaps:0 ScheduledReds:1 AssignedMaps:0 AssignedReds:0 CompletedMaps:1 CompletedReds:0 ContAlloc:1 ContRel:0 HostLocal:1 RackLocal:0
    2015-12-30 17:31:11,908 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.TaskAttemptImpl: Diagnostics report from attempt_1451360650431_0228_m_000000_0: Container killed by the ApplicationMaster.
    Container killed on request. Exit code is 143
    Container exited with a non-zero exit code 143</pre></td></tr></table><p class="theCode" style="display:none;">2015-12-30 17:31:09,994 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.TaskAttemptImpl: attempt_1451360650431_0228_m_000000_0 TaskAttempt Transitioned from RUNNING to SUCCESS_CONTAINER_CLEANUP
    2015-12-30 17:31:09,995 INFO [ContainerLauncher #1] org.apache.hadoop.mapreduce.v2.app.launcher.ContainerLauncherImpl: Processing the event EventType: CONTAINER_REMOTE_CLEANUP for container container_1451360650431_0228_01_000002 taskAttempt attempt_1451360650431_0228_m_000000_0
    2015-12-30 17:31:09,995 INFO [ContainerLauncher #1] org.apache.hadoop.mapreduce.v2.app.launcher.ContainerLauncherImpl: KILLING attempt_1451360650431_0228_m_000000_0
    2015-12-30 17:31:09,995 INFO [ContainerLauncher #1] org.apache.hadoop.yarn.client.api.impl.ContainerManagementProtocolProxy: Opening proxy : uaerouter2-vm02:8041
    2015-12-30 17:31:10,012 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.TaskAttemptImpl: attempt_1451360650431_0228_m_000000_0 TaskAttempt Transitioned from SUCCESS_CONTAINER_CLEANUP to SUCCEEDED
    2015-12-30 17:31:10,020 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.TaskImpl: Task succeeded with attempt attempt_1451360650431_0228_m_000000_0
    2015-12-30 17:31:10,021 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.TaskImpl: task_1451360650431_0228_m_000000 Task Transitioned from RUNNING to SUCCEEDED
    2015-12-30 17:31:10,023 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.JobImpl: Num completed Tasks: 1
    2015-12-30 17:31:10,895 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Before Scheduling: PendingReds:1 ScheduledMaps:0 ScheduledReds:0 AssignedMaps:1 AssignedReds:0 CompletedMaps:1 CompletedReds:0 ContAlloc:1 ContRel:0 HostLocal:1 RackLocal:0
    2015-12-30 17:31:10,898 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Recalculating schedule, headroom=&lt;memory:14336, vCores:14&gt;
    2015-12-30 17:31:10,898 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Reduce slow start threshold reached. Scheduling reduces.
    2015-12-30 17:31:10,898 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: All maps assigned. Ramping up all remaining reduces:1
    2015-12-30 17:31:10,898 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: After Scheduling: PendingReds:0 ScheduledMaps:0 ScheduledReds:1 AssignedMaps:1 AssignedReds:0 CompletedMaps:1 CompletedReds:0 ContAlloc:1 ContRel:0 HostLocal:1 RackLocal:0
    2015-12-30 17:31:11,906 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerRequestor: getResources() for application_1451360650431_0228: ask=1 release= 0 newContainers=0 finishedContainers=1 resourcelimit=&lt;memory:15360, vCores:15&gt; knownNMs=2
    2015-12-30 17:31:11,906 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Received completed container container_1451360650431_0228_01_000002
    2015-12-30 17:31:11,907 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: After Scheduling: PendingReds:0 ScheduledMaps:0 ScheduledReds:1 AssignedMaps:0 AssignedReds:0 CompletedMaps:1 CompletedReds:0 ContAlloc:1 ContRel:0 HostLocal:1 RackLocal:0
    2015-12-30 17:31:11,908 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.TaskAttemptImpl: Diagnostics report from attempt_1451360650431_0228_m_000000_0: Container killed by the ApplicationMaster.
    Container killed on request. Exit code is 143
    Container exited with a non-zero exit code 143</p></div>
    ";}
categories:
  - hadoop
tags:
  - 143
  - hadoop
  - issue

---
之前发现在map任务里面经常看到Container killed by the ApplicationMaster，挺奇怪，不过任务最终是成功的，就没怎么管。不过最近测试集群跑的任务报143错误，还是重新看一下这个问题。
分析版本：hadoop cdh5.4
## 错误日志

<pre lang="other" escaped="true">2015-12-30 17:31:09,994 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.TaskAttemptImpl: attempt_1451360650431_0228_m_000000_0 TaskAttempt Transitioned from RUNNING to SUCCESS_CONTAINER_CLEANUP
2015-12-30 17:31:09,995 INFO [ContainerLauncher #1] org.apache.hadoop.mapreduce.v2.app.launcher.ContainerLauncherImpl: Processing the event EventType: CONTAINER_REMOTE_CLEANUP for container container_1451360650431_0228_01_000002 taskAttempt attempt_1451360650431_0228_m_000000_0
2015-12-30 17:31:09,995 INFO [ContainerLauncher #1] org.apache.hadoop.mapreduce.v2.app.launcher.ContainerLauncherImpl: KILLING attempt_1451360650431_0228_m_000000_0
2015-12-30 17:31:09,995 INFO [ContainerLauncher #1] org.apache.hadoop.yarn.client.api.impl.ContainerManagementProtocolProxy: Opening proxy : uaerouter2-vm02:8041
2015-12-30 17:31:10,012 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.TaskAttemptImpl: attempt_1451360650431_0228_m_000000_0 TaskAttempt Transitioned from SUCCESS_CONTAINER_CLEANUP to SUCCEEDED
2015-12-30 17:31:10,020 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.TaskImpl: Task succeeded with attempt attempt_1451360650431_0228_m_000000_0
2015-12-30 17:31:10,021 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.TaskImpl: task_1451360650431_0228_m_000000 Task Transitioned from RUNNING to SUCCEEDED
2015-12-30 17:31:10,023 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.JobImpl: Num completed Tasks: 1
2015-12-30 17:31:10,895 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Before Scheduling: PendingReds:1 ScheduledMaps:0 ScheduledReds:0 AssignedMaps:1 AssignedReds:0 CompletedMaps:1 CompletedReds:0 ContAlloc:1 ContRel:0 HostLocal:1 RackLocal:0
2015-12-30 17:31:10,898 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Recalculating schedule, headroom=&lt;memory:14336, vCores:14&gt;
2015-12-30 17:31:10,898 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Reduce slow start threshold reached. Scheduling reduces.
2015-12-30 17:31:10,898 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: All maps assigned. Ramping up all remaining reduces:1
2015-12-30 17:31:10,898 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: After Scheduling: PendingReds:0 ScheduledMaps:0 ScheduledReds:1 AssignedMaps:1 AssignedReds:0 CompletedMaps:1 CompletedReds:0 ContAlloc:1 ContRel:0 HostLocal:1 RackLocal:0
2015-12-30 17:31:11,906 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerRequestor: getResources() for application_1451360650431_0228: ask=1 release= 0 newContainers=0 finishedContainers=1 resourcelimit=&lt;memory:15360, vCores:15&gt; knownNMs=2
2015-12-30 17:31:11,906 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: Received completed container container_1451360650431_0228_01_000002
2015-12-30 17:31:11,907 INFO [RMCommunicator Allocator] org.apache.hadoop.mapreduce.v2.app.rm.RMContainerAllocator: After Scheduling: PendingReds:0 ScheduledMaps:0 ScheduledReds:1 AssignedMaps:0 AssignedReds:0 CompletedMaps:1 CompletedReds:0 ContAlloc:1 ContRel:0 HostLocal:1 RackLocal:0
2015-12-30 17:31:11,908 INFO [AsyncDispatcher event handler] org.apache.hadoop.mapreduce.v2.app.job.impl.TaskAttemptImpl: Diagnostics report from attempt_1451360650431_0228_m_000000_0: Container killed by the ApplicationMaster.
Container killed on request. Exit code is 143
Container exited with a non-zero exit code 143
</pre>
分析一下错误日志
  1. 其中一个mapper任务完成，发送事件TaskAttemptEventType.TA_DONE
  2. 执行CleanupContainerTransition，取消taskAttemptListener监听，发送事件 ContainerLauncher.EventType.CONTAINER\_REMOTE\_CLEANUP给containerLauncher
  3. containerLauncher执行kill命令，但判断container状态还没完成，让container kill掉
  4. container还没有退出，被强制kill掉，所以有一个143的错误
  5. TaskAttempt状态由RUNNING 转为 SUCCESS\_CONTAINER\_CLEANUP
  6. kill了之后发送事件TaskAttemptEventType.TA\_CONTAINER\_CLEANED
  7. TaskAttempt状态由SUCCESS\_CONTAINER\_CLEANUP转为SUCCEEDED
这里会有143的错误的原因是没等到container退出，就发起命令kill掉它了。简单的改法是等待几秒后再去kill它，但是到底要等几秒，每个都要等几秒拖慢了集群。还是看大神是怎么改的。
## 分析补丁

找到 <a href="https://issues.apache.org/jira/browse/MAPREDUCE-5465" target="_blank">MAPREDUCE-5465</a> 这个补丁。
在这个补丁里，在RUNNING -> SUCCESS\_CONTAINER\_CLEANUP 状态转换中，插入了一个状态 SUCCESS\_FINISHING\_CONTAINER （成功的场景，失败有另一个状态）。引入这个状态就是为了等container自己退出。
  1. 其中一个mapper任务完成，发送事件TaskAttemptEventType.TA_DONE
  2. 向TaskAttemptFinishingMonitor注册(这个类用来避免container一直不退出，之后说)，尽管container这时还没退出，还是发送TaskEventType.T\_ATTEMPT\_SUCCEEDED事件
  3. 状态由RUNNING 转为 SUCCESS\_FINISHING\_CONTAINER
  4. 等待container退出（依赖nodemanager发现container退出，汇报给RM，然后再传给AM）
  5. AM知道container退出后，检查退出状态，如果是被终止的，就发送TaskAttemptEventType.TA\_KILL，否则发送TaskAttemptEventType.TA\_CONTAINER_COMPLETED
  6. 如果事件是TA\_KILL，状态则会变成SUCCESS\_CONTAINER\_CLEANUP或者KILL\_CONTAINER\_CLEANUP。SUCCESS\_CONTAINER_CLEANUP可以再转换为SUCCESSED
  7. 如果事件是TA\_CONTAINER\_COMPLETED，状态就变成SUCCESSED了
另外还会收到事件TA\_CONTAINER\_CLEANED，有条件才会发这个事件的，看注释，好像是等价于TA\_CONTAINER\_COMPLETED（好烦）
向TaskAttemptFinishingMonitor注册是这里设定了一个定时器，如果超过时间container都还没有退出，这个Monitor就会发起TA\_TIMED\_OUT的操作了，会把状态由 SUCCESS\_FINISHING\_CONTAINER 转为 SUCCESS\_CONTAINER\_CLEANUP，通过kill的方式清理。
同样，这里还会对失败的taskattempt也做同样的处理，会有对应的状态。