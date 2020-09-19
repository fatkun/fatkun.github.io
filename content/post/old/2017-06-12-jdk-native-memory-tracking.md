---
title: JDK Native Memory Tracking
author: fatkun
type: post
date: 2017-06-12T07:42:07+00:00
url: /2017/06/jdk-native-memory-tracking.html
categories:
  - J2EE
tags:
  - jdk

---
command line option: -XX:NativeMemoryTracking=summary or -XX:NativeMemoryTracking=detail
jcmd ${PID} VM.native_memory summary
https://docs.oracle.com/javase/8/docs/technotes/guides/troubleshoot/tooldescr007.html