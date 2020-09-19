---
title: Extjs combobox下拉框模糊匹配
author: fatkun
type: post
date: 2011-10-21T17:30:28+00:00
url: /2011/10/extjs-combobox-filter.html
duoshuo_thread_id:
  - 6300408819943998209
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:5082:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="js" style="font-family:monospace;">// 判断某个值str是否存在store里,field是store的字段
    var checkIfInStore = function(str, store, field, ignoreCase) {
        var count = store.getCount();
        for( var i = 0; i &lt; count; i++) {
            var val = store.getAt(i).get(field);
            if (ignoreCase) {
                str = str.toUpperCase();
                val = val.toUpperCase();
            }
            if (str == val) {
                return true;
            }
        }
        return false;
    };
    &nbsp;
    var ComboSearchPlugin = {
        init: function(combo) {
            combo.addListener('blur', function(combo) {
                // 如果没有写完整则设置为空
                var isValid = checkIfInStore(combo.getRawValue(), combo.store, combo.displayField, false);
                if (!isValid) {
                    combo.setValue('');
                }
            });
    &nbsp;
            combo.addListener('beforequery', function(qe) {
                var combo = qe.combo;
                var q = qe.query;
                var forceAll = qe.forceAll;
                if (forceAll === true || (q.length &gt;= this.minChars)) {
                    if (this.lastQuery !== q) {
                        this.lastQuery = q;
                        if (this.mode == 'local') {
                            this.selectedIndex = -1;
                            if (forceAll) {
                                this.store.clearFilter();
                            } else {
                                // 检索的正则
                                var regExp = new RegExp(&quot;.*&quot; + q + &quot;.*&quot;, &quot;i&quot;);
                                // 执行检索
                                this.store.filterBy(function(record, id) {
                                    // 得到每个record的项目名称值
                                    var text = record.get(combo.displayField);
                                    return regExp.test(text);
                                });
                            }
                            this.onLoad();
                        } else {
                            this.store.baseParams[this.queryParam] = q;
                            this.store.load({
                                params: this.getParams(q)
                            });
                            this.expand();
                        }
                    } else {
                        this.selectedIndex = -1;
                        this.onLoad();
                    }
                }
                return false;
            });
        }
    };</pre></td></tr></table><p class="theCode" style="display:none;">// 判断某个值str是否存在store里,field是store的字段
    var checkIfInStore = function(str, store, field, ignoreCase) {
        var count = store.getCount();
        for( var i = 0; i &lt; count; i++) {
            var val = store.getAt(i).get(field);
            if (ignoreCase) {
                str = str.toUpperCase();
                val = val.toUpperCase();
            }
            if (str == val) {
                return true;
            }
        }
        return false;
    };
    
    var ComboSearchPlugin = {
        init: function(combo) {
            combo.addListener('blur', function(combo) {
                // 如果没有写完整则设置为空
                var isValid = checkIfInStore(combo.getRawValue(), combo.store, combo.displayField, false);
                if (!isValid) {
                    combo.setValue('');
                }
            });
    
            combo.addListener('beforequery', function(qe) {
                var combo = qe.combo;
                var q = qe.query;
                var forceAll = qe.forceAll;
                if (forceAll === true || (q.length &gt;= this.minChars)) {
                    if (this.lastQuery !== q) {
                        this.lastQuery = q;
                        if (this.mode == 'local') {
                            this.selectedIndex = -1;
                            if (forceAll) {
                                this.store.clearFilter();
                            } else {
                                // 检索的正则
                                var regExp = new RegExp(&quot;.*&quot; + q + &quot;.*&quot;, &quot;i&quot;);
                                // 执行检索
                                this.store.filterBy(function(record, id) {
                                    // 得到每个record的项目名称值
                                    var text = record.get(combo.displayField);
                                    return regExp.test(text);
                                });
                            }
                            this.onLoad();
                        } else {
                            this.store.baseParams[this.queryParam] = q;
                            this.store.load({
                                params: this.getParams(q)
                            });
                            this.expand();
                        }
                    } else {
                        this.selectedIndex = -1;
                        this.onLoad();
                    }
                }
                return false;
            });
        }
    };</p></div>
    ";}
categories:
  - 网页前端
tags:
  - Combobox
  - extjs
  - js

---
Ext中的combobox有属性typeAhead：true 可以实现模糊匹配，但是是从开始匹配的，如果需要自定的的匹配，则需要监听beforequery方法，实现自己的匹配查询方法：
<pre escaped="true" lang="js">// 判断某个值str是否存在store里,field是store的字段
var checkIfInStore = function(str, store, field, ignoreCase) {
    var count = store.getCount();
    for( var i = 0; i &lt; count; i++) {
        var val = store.getAt(i).get(field);
        if (ignoreCase) {
            str = str.toUpperCase();
            val = val.toUpperCase();
        }
        if (str == val) {
            return true;
        }
    }
    return false;
};

var ComboSearchPlugin = {
    init: function(combo) {
        combo.addListener('blur', function(combo) {
            // 如果没有写完整则设置为空
            var isValid = checkIfInStore(combo.getRawValue(), combo.store, combo.displayField, false);
            if (!isValid) {
                combo.setValue('');
            }
        });

        combo.addListener('beforequery', function(qe) {
            var combo = qe.combo;
            var q = qe.query;
            var forceAll = qe.forceAll;
            if (forceAll === true || (q.length &gt;= this.minChars)) {
                if (this.lastQuery !== q) {
                    this.lastQuery = q;
                    if (this.mode == 'local') {
                        this.selectedIndex = -1;
                        if (forceAll) {
                            this.store.clearFilter();
                        } else {
                            // 检索的正则
                            var regExp = new RegExp(".*" + q + ".*", "i");
                            // 执行检索
                            this.store.filterBy(function(record, id) {
                                // 得到每个record的项目名称值
                                var text = record.get(combo.displayField);
                                return regExp.test(text);
                            });
                        }
                        this.onLoad();
                    } else {
                        this.store.baseParams[this.queryParam] = q;
                        this.store.load({
                            params: this.getParams(q)
                        });
                        this.expand();
                    }
                } else {
                    this.selectedIndex = -1;
                    this.onLoad();
                }
            }
            return false;
        });
    }
};</pre>
参考文章：http://weibaojun.iteye.com/blog/1098731  
原文我试了一下有问题，第一次输入时会不显示结果，主要差别在onLoad上