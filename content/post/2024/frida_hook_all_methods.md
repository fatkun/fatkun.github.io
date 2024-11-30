---
title: "frida Hook一个类下的所有方法"
date: 2024-11-30T14:51:54+08:00
tags: [android, 逆向]
categories: [android]
author: "fatkun"
draft: false
typora-root-url: ./..\..\..\static
---

代码来自于[ZenTracer](https://github.com/hluwa/ZenTracer/blob/master/trace.js)这个项目，获取类的地方做了修改。

```js
function log(text) {
    var packet = {
        'cmd': 'log',
        'data': text
    };
    send("ZenTracer:::" + JSON.stringify(packet))
}

function enter(tid, tname, cls, method, args) {
    var packet = {
        'cmd': 'enter',
        'data': [tid, tname, cls, method, args]
    };
    send("ZenTracer:::" + JSON.stringify(packet))
}

function exit(tid, retval) {
    var packet = {
        'cmd': 'exit',
        'data': [tid, retval]
    };
    send("ZenTracer:::" + JSON.stringify(packet))
}

function getTid() {
    var Thread = Java.use("java.lang.Thread")
    return Thread.currentThread().getId();
}

function getTName() {
    var Thread = Java.use("java.lang.Thread")
    return Thread.currentThread().getName();
}

function traceClass(target) {
    try {
        var clsname = target.class.getName();
        var methods = target.class.getDeclaredMethods();
        // log(methods);
        methods.forEach(function (method) {
            var methodName = method.getName();
            var overloads = target[methodName].overloads;
            overloads.forEach(function (overload) {
                var proto = "(";
                overload.argumentTypes.forEach(function (type) {
                    proto += type.className + ", ";
                });
                if (proto.length > 1) {
                    proto = proto.substr(0, proto.length - 2);
                }
                proto += ")";
                log("hooking: " + clsname + "." + methodName + proto);
                overload.implementation = function () {
                    var args = [];
                    var tid = getTid();
                    var tName = getTName();
                    for (var j = 0; j < arguments.length; j++) {
                        args[j] = arguments[j] + ""
                    }
                    enter(tid, tName, clsname, methodName + proto, args);
                    var retval = this[methodName].apply(this, arguments);
                    exit(tid, "" + retval);
                    return retval;
                }
            });
        });
    } catch (e) {
        console.error(e)
        // var stackTrace = Java.use('android.util.Log').getStackTraceString(Java.use('java.lang.Exception').$new());
        // console.log(stackTrace);
        log("'" + clsname + "' hook fail: " + e)
    }
}

Java.perform(function(){
    Java.choose("dalvik.system.PathClassLoader",{
        onMatch: function(instance){
            var loader = Java.ClassFactory.get(instance)
            try {
                var clazz = loader.use("com.douyu.sdk.ad.douyu.video.AdVideoPlayerPresenter")
                console.log("-------------clazz", clazz)
                traceClass(clazz)
                return "stop"
            }catch(e){
                //console.log("next")
                //console.log(e)
            }
        },
        onComplete:function(){
            console.log("Done")
        }
    })
})

```