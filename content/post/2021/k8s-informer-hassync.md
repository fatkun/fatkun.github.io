---
title: "K8s Informer HasSync"
date: 2021-04-18T17:30:28+08:00
tags: []
categories: []
author: "fatkun"
draft: true
---

# 背景

K8S中的informer中HasSynced到底表示什么？



# 分析

HasSynced的注释是这样写的，如果拿到至少一个列表后返回true。

```
HasSynced returns true if the shared informer's store has been informed by at least one full LIST of the authoritative state of the informer's object collection.  This is unrelated to "resync".
```

一般我们使用informer的时候，会监听一些对象，那HasSynced是否会等待这些做完才返回呢？



```go
// HasSynced returns true if an Add/Update/Delete/AddIfNotPresent are called first,
// or an Update called first but the first batch of items inserted by Replace() has been popped
func (f *DeltaFIFO) HasSynced() bool {
	f.lock.Lock()
	defer f.lock.Unlock()
	return f.populated && f.initialPopulationCount == 0
}
```



在func (f *DeltaFIFO) Pop(process PopProcessFunc)的时候负责initialPopulationCount的减少，并且这里有锁，能保证在调用完process(item)才返回。



但是事件传递有个缓冲池，事件是异步处理。



```go
func (p *processorListener) pop() {
	defer utilruntime.HandleCrash()
	defer close(p.nextCh) // Tell .run() to stop

	var nextCh chan<- interface{}
	var notification interface{}
	for {
		select {
		case nextCh <- notification:
			// Notification dispatched
			var ok bool
			notification, ok = p.pendingNotifications.ReadOne()
			if !ok { // Nothing to pop
				nextCh = nil // Disable this select case
			}
		case notificationToAdd, ok := <-p.addCh:
			if !ok {
				return
			}
			if notification == nil { // No notification to pop (and pendingNotifications is empty)
				// Optimize the case - skip adding to pendingNotifications
				notification = notificationToAdd
				nextCh = p.nextCh
			} else { // There is already a notification waiting to be dispatched
				p.pendingNotifications.WriteOne(notificationToAdd)
			}
		}
	}
}
```





# 结论

HasSynced=true时，只能保证store中的数据已经加载第一批，事件处理是异步的，无法保证完成。

