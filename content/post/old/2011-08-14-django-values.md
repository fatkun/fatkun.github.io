---
title: 'Django values(*fields) 如何使用'
author: fatkun
type: post
date: 2011-08-14T09:08:12+00:00
url: /2011/08/django-values.html
duoshuo_thread_id:
  - 6300408819281298177
wp-syntax-cache-content:
  - |
    a:6:{i:1;s:1388:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;">AppDef.<span style="color: black;">objects</span>.<span style="color: black;">values</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
    <span style="color: black;">&#91;</span><span style="color: black;">&#123;</span><span style="color: #483d8b;">'creator'</span>: u<span style="color: #483d8b;">'admin'</span><span style="color: #66cc66;">,</span> <span style="color: #483d8b;">'apptype_name'</span>: u<span style="color: #483d8b;">'uc3g'</span><span style="color: #66cc66;">,</span> <span style="color: #483d8b;">'apptype_chn_name'</span>: u<span style="color: #483d8b;">'3G<span style="color: #000099; font-weight: bold;">\u</span>95e8<span style="color: #000099; font-weight: bold;">\u</span>6237'</span><span style="color: #66cc66;">,</span> <span style="color: #483d8b;">'note'</span>: u<span style="color: #483d8b;">''</span><span style="color: #66cc66;">,</span> ...<span style="color: black;">&#125;</span><span style="color: #66cc66;">,</span>...<span style="color: black;">&#93;</span></pre></td></tr></table><p class="theCode" style="display:none;">AppDef.objects.values()
    [{'creator': u'admin', 'apptype_name': u'uc3g', 'apptype_chn_name': u'3G\u95e8\u6237', 'note': u'', ...},...]</p></div>
    ";i:2;s:801:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;">AppDef.<span style="color: black;">objects</span>.<span style="color: black;">values</span><span style="color: black;">&#40;</span><span style="color: #483d8b;">'apptype_name'</span><span style="color: black;">&#41;</span>
    <span style="color: black;">&#91;</span><span style="color: black;">&#123;</span><span style="color: #483d8b;">'apptype_name'</span>: u<span style="color: #483d8b;">'uc3g'</span><span style="color: black;">&#125;</span><span style="color: #66cc66;">,</span>...<span style="color: black;">&#93;</span></pre></td></tr></table><p class="theCode" style="display:none;">AppDef.objects.values('apptype_name')
    [{'apptype_name': u'uc3g'},...]</p></div>
    ";i:3;s:1157:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;">AppDef.<span style="color: black;">objects</span>.<span style="color: #008000;">filter</span><span style="color: black;">&#40;</span>pk<span style="color: #66cc66;">=</span><span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span>.<span style="color: black;">values</span><span style="color: black;">&#40;</span><span style="color: #483d8b;">'apptype_name'</span><span style="color: black;">&#41;</span>
    AppDef.<span style="color: black;">objects</span>.<span style="color: black;">values</span><span style="color: black;">&#40;</span><span style="color: #483d8b;">'apptype_name'</span><span style="color: black;">&#41;</span>.<span style="color: #008000;">filter</span><span style="color: black;">&#40;</span>pk<span style="color: #66cc66;">=</span><span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">AppDef.objects.filter(pk=1).values('apptype_name')
    AppDef.objects.values('apptype_name').filter(pk=1)</p></div>
    ";i:4;s:1195:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;">LogTypeDef.<span style="color: black;">objects</span>.<span style="color: #008000;">filter</span><span style="color: black;">&#40;</span>pk<span style="color: #66cc66;">=</span><span style="color: #ff4500;">6</span><span style="color: black;">&#41;</span>.<span style="color: black;">values</span><span style="color: black;">&#40;</span><span style="color: #483d8b;">'pk'</span><span style="color: #66cc66;">,</span> <span style="color: #483d8b;">'app__apptype_name'</span><span style="color: black;">&#41;</span>
    <span style="color: black;">&#91;</span><span style="color: black;">&#123;</span><span style="color: #483d8b;">'pk'</span>: 6L<span style="color: #66cc66;">,</span> <span style="color: #483d8b;">'app__apptype_name'</span>: u<span style="color: #483d8b;">'wapsearch'</span><span style="color: black;">&#125;</span><span style="color: black;">&#93;</span></pre></td></tr></table><p class="theCode" style="display:none;">LogTypeDef.objects.filter(pk=6).values('pk', 'app__apptype_name')
    [{'pk': 6L, 'app__apptype_name': u'wapsearch'}]</p></div>
    ";i:5;s:1882:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;">LogTypeDef.<span style="color: black;">objects</span>.<span style="color: #008000;">filter</span><span style="color: black;">&#40;</span>pk<span style="color: #66cc66;">=</span><span style="color: #ff4500;">6</span><span style="color: black;">&#41;</span>.<span style="color: black;">values</span><span style="color: black;">&#40;</span><span style="color: #483d8b;">'pk'</span><span style="color: #66cc66;">,</span> <span style="color: #483d8b;">'app_id'</span><span style="color: black;">&#41;</span>
    LogTypeDef.<span style="color: black;">objects</span>.<span style="color: #008000;">filter</span><span style="color: black;">&#40;</span>pk<span style="color: #66cc66;">=</span><span style="color: #ff4500;">6</span><span style="color: black;">&#41;</span>.<span style="color: black;">values</span><span style="color: black;">&#40;</span><span style="color: #483d8b;">'pk'</span><span style="color: #66cc66;">,</span> <span style="color: #483d8b;">'app'</span><span style="color: black;">&#41;</span>
    LogTypeDef.<span style="color: black;">objects</span>.<span style="color: #008000;">filter</span><span style="color: black;">&#40;</span>pk<span style="color: #66cc66;">=</span><span style="color: #ff4500;">6</span><span style="color: black;">&#41;</span>.<span style="color: black;">values</span><span style="color: black;">&#40;</span><span style="color: #483d8b;">'pk'</span><span style="color: #66cc66;">,</span> <span style="color: #483d8b;">'app__id'</span><span style="color: black;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">LogTypeDef.objects.filter(pk=6).values('pk', 'app_id')
    LogTypeDef.objects.filter(pk=6).values('pk', 'app')
    LogTypeDef.objects.filter(pk=6).values('pk', 'app__id')</p></div>
    ";i:6;s:797:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: black;">&#91;</span><span style="color: black;">&#123;</span>pk: <span style="color: #ff4500;">6</span><span style="color: #66cc66;">,</span> app_id: <span style="color: #ff4500;">2</span><span style="color: black;">&#125;</span><span style="color: #66cc66;">,</span> <span style="color: black;">&#123;</span>pk: <span style="color: #ff4500;">6</span><span style="color: #66cc66;">,</span> app_id: <span style="color: #ff4500;">3</span><span style="color: black;">&#125;</span><span style="color: black;">&#93;</span></pre></td></tr></table><p class="theCode" style="display:none;">[{pk: 6, app_id: 2}, {pk: 6, app_id: 3}]</p></div>
    ";}
categories:
  - python
tags:
  - django
  - python
  - values

---
<div>  <p>    官方文档:<a href="https://docs.djangoproject.com/en/1.3/ref/models/querysets/#values">https://docs.djangoproject.com/en/1.3/ref/models/querysets/#values</a>  </p>
  <h1>    1. values(*fields)  </h1>
  <p>    这个方法返回的是ValuesQuerySet,是QuerySet 的子类，也就是说，你可以用QuerySet里的方法。 需要注意的是，返回的不是list，不要直接当list来用了。对ValuesQuerySet遍历，每一个元素是“字典”dict。  </p>
  <p>    当不传入参数时，返回这个model的所有字段  </p>
  <pre escaped="true" lang="python">AppDef.objects.values()
[{'creator': u'admin', 'apptype_name': u'uc3g', 'apptype_chn_name': u'3G\u95e8\u6237', 'note': u'', ...},...]</pre>
  <p>    当传入参数时，只会列出你指定的参数  </p>
  <pre escaped="true" lang="python">AppDef.objects.values('apptype_name')
[{'apptype_name': u'uc3g'},...]</pre>
  <p>    也可以加上<span style="font-family: 'Courier New';">filter</span><span style="font-family: 宋体;">，</span><span style="font-family: 'Courier New';">filter</span><span style="font-family: 宋体;">在前或者后面都是一样的</span>  </p>
  <pre escaped="true" lang="python">AppDef.objects.filter(pk=1).values('apptype_name')
AppDef.objects.values('apptype_name').filter(pk=1)</pre>
  <p>    如果想把关联的字段也一起查出来<br /> OneToOneField, ForeignKey 和ManyToManyField 关系的都可以。<br /> ManyToManyField 在Django1.3<span style="font-family: 微软雅黑;">版后才支持</span><br /> LogTypeDef定义了一个app<span style="font-family: 宋体;">的</span><span style="font-family: 'Courier New';">ForeignKey</span>  </p>
  <pre escaped="true" lang="python">LogTypeDef.objects.filter(pk=6).values('pk', 'app__apptype_name')
[{'pk': 6L, 'app__apptype_name': u'wapsearch'}]</pre>
  <p>    如果你只想拿到app_id<span style="font-family: 宋体;">，可以这样</span><br /> 下面三种方法都是一样的，只是返回的结果名字对应你的查询语句  </p>
  <pre escaped="true" lang="python">LogTypeDef.objects.filter(pk=6).values('pk', 'app_id')
LogTypeDef.objects.filter(pk=6).values('pk', 'app')
LogTypeDef.objects.filter(pk=6).values('pk', 'app__id')</pre>
  <p>    注意在关联关系为多对多的时候，它只会帮你一条一条的列出来，而不会帮你合并为一个<span style="font-family: 'Courier New';">list</span><span style="font-family: 宋体;">。</span><br /> 例如会返回类型的结果：同一个<span style="font-family: 'Courier New';">pk</span><span style="font-family: 宋体;">并不会帮你合并</span><span style="font-family: 'Courier New';">app_id</span>  </p>
  <pre escaped="true" lang="python">[{pk: 6, app_id: 2}, {pk: 6, app_id: 3}]</pre>
  <h1>    2. 注意事项  </h1>
  <p>    当同时使用distinct()和values()，需要注意order_by() (或者默认 model ordering) ，会自动加入select 中作为distinct项，所以返回的结果你以为是重复的，其实是order by的字段没列出来。<br /> 如果在extra() 之后用values()，一定要把extra用到的字段也加进来；如果extra()在values()之后，extra的字段会自动加进select。<br /> Because <a href="https://docs.djangoproject.com/en/1.3/ref/models/fields/#django.db.models.ManyToManyField">ManyToManyField</a> attributes and reverse relations can have multiple related rows, including these can have a multiplier effect on the size of your result set. This will be especially pronounced if you include multiple such fields in your values() query, in which case all possible combinations will be returned. (<span style="font-family: 微软雅黑;">这个不太懂什么意思，应该是当</span><span style="font-family: Arial;">values</span><span style="font-family: 微软雅黑;">有多个</span><span style="font-family: Arial;">manytomanyfield</span><span style="font-family: 微软雅黑;">的时候，会尽量合并一些</span><span style="font-family: Arial;">)</span>  </p>
  <h1>    3. 适用范围  </h1>
  <p>    l 只需要返回<span style="font-family: Arial;">dict</span><span style="font-family: 微软雅黑;">，而不需要返回</span><span style="font-family: Arial;">model object</span><span style="font-family: 微软雅黑;">。</span><br /> l 只需要返回简单的数据（包括层次简单）  </p>
  <h1>    4. Values_list  </h1>
  <p>    和<span style="font-family: Arial;">values</span><span style="font-family: 微软雅黑;">一样，只是返回的不是字典而是元组。</span> </div>