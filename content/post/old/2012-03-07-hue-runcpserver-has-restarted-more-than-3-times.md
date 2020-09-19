---
title: hue runcpserver has restarted more than 3 times
author: fatkun
type: post
date: 2012-03-06T17:07:38+00:00
url: /2012/03/hue-runcpserver-has-restarted-more-than-3-times.html
duoshuo_thread_id:
  - 6300408840592556801
categories:
  - 未分类
tags:
  - hue

---
运行hue时，~/hue/build/env/bin$ ./supervisor 遇到这个错误，查看logs可以看到这句：
> runcpserver has restarted more than 3 times
## 解决方法

更改hue/desktop/conf/hue.ini配置  
\# Set to true to use CherryPy as the webserver, set to false  
\# to use Spawning as the webserver. Defaults to Spawning if  
\# key is not specified.  
use\_cherrypy\_server = true
去掉注释并改为true  
默认为Spawning，不知道我错误的原因。。不过盖茨用cherrypy就正常了。  
如果需要用beeswax还需要配置hue_beeswax.ini，把注释去掉就可以了。