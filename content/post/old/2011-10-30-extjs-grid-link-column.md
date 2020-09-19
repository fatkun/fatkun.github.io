---
title: 在Extjs Grid扩展一个链接按钮列
author: fatkun
type: post
date: 2011-10-30T06:19:29+00:00
url: /2011/10/extjs-grid-link-column.html
duoshuo_thread_id:
  - 6300408820002718466
wp-syntax-cache-content:
  - |
    a:2:{i:1;s:5610:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="js" style="font-family:monospace;">/*!
     * Ext JS Library 3.3.1
     * Copyright(c) 2006-2010 Sencha Inc.
     * licensing@sencha.com
     * http://www.sencha.com/license
     */
    Ext.grid.LinkColumn = Ext.extend(Ext.grid.Column, {
        header: '&amp;#160;',
        linkIdRe: /x-link-col-(\d+)/,
    &nbsp;
        constructor: function(cfg) {
            var me = this,
                items = cfg.items || (me.items = [me]),
                l = items.length,
                i,
                item;
    &nbsp;
            Ext.grid.LinkColumn.superclass.constructor.call(me, cfg);
    &nbsp;
            me.renderer = function(v, meta) {
    //          Allow a configured renderer to create initial value (And set the other values in the &quot;metadata&quot; argument!)
                v = Ext.isFunction(cfg.renderer) ? cfg.renderer.apply(this, arguments)||'' : '';
    &nbsp;
                meta.css += ' x-link-col-cell';
                for (i = 0; i &lt; l; i++) {
                    item = items[i];
                    v += '&lt;a href=&quot;javascript:;&quot; class=&quot;x-link-col-icon x-link-col-' + String(i) + ' ' + (Ext.isFunction(item.getClass) ? item.getClass.apply(item.scope||this.scope||this, arguments) : '') + '&quot;' +
                        ((item.tooltip) ? ' ext:qtip=&quot;' + item.tooltip + '&quot;' : '') + '&gt;' + (item.text||'') + '&lt;/a&gt;';
                    if (i &lt; l - 1) v += '&amp;nbsp;&amp;nbsp;&amp;nbsp;&amp;nbsp;';
                }
                return v;
            };
        },
    &nbsp;
        destroy: function() {
            delete this.items;
            delete this.renderer;
            return Ext.grid.LinkColumn.superclass.destroy.apply(this, arguments);
        },
    &nbsp;
        /**
         * @private
         * Process and refire events routed from the GridView's processEvent method.
         * Also fires any configured click handlers. By default, cancels the mousedown event to prevent selection.
         * Returns the event handler's status to allow cancelling of GridView's bubbling process.
         */
        processEvent : function(name, e, grid, rowIndex, colIndex){
            var m = e.getTarget().className.match(this.linkIdRe),
                item, fn;
            if (m &amp;&amp; (item = this.items[parseInt(m[1], 10)])) {
                if (name == 'click') {
                    (fn = item.handler || this.handler) &amp;&amp; fn.call(item.scope||this.scope||this, grid, rowIndex, colIndex, item, e);
                } else if ((name == 'mousedown') &amp;&amp; (item.stopSelection !== false)) {
                    return false;
                }
            }
            return Ext.grid.LinkColumn.superclass.processEvent.apply(this, arguments);
        }
    });
    &nbsp;
    //register ptype
    Ext.preg('linkcolumn', Ext.grid.LinkColumn);
    &nbsp;
    // register Column xtype
    Ext.grid.Column.types.linkcolumn = Ext.grid.LinkColumn;</pre></td></tr></table><p class="theCode" style="display:none;">/*!
     * Ext JS Library 3.3.1
     * Copyright(c) 2006-2010 Sencha Inc.
     * licensing@sencha.com
     * http://www.sencha.com/license
     */
    Ext.grid.LinkColumn = Ext.extend(Ext.grid.Column, {
        header: '&amp;#160;',
        linkIdRe: /x-link-col-(\d+)/,
    
        constructor: function(cfg) {
            var me = this,
                items = cfg.items || (me.items = [me]),
                l = items.length,
                i,
                item;
    
            Ext.grid.LinkColumn.superclass.constructor.call(me, cfg);
    
            me.renderer = function(v, meta) {
    //          Allow a configured renderer to create initial value (And set the other values in the &quot;metadata&quot; argument!)
                v = Ext.isFunction(cfg.renderer) ? cfg.renderer.apply(this, arguments)||'' : '';
    
                meta.css += ' x-link-col-cell';
                for (i = 0; i &lt; l; i++) {
                    item = items[i];
                    v += '&lt;a href=&quot;javascript:;&quot; class=&quot;x-link-col-icon x-link-col-' + String(i) + ' ' + (Ext.isFunction(item.getClass) ? item.getClass.apply(item.scope||this.scope||this, arguments) : '') + '&quot;' +
                        ((item.tooltip) ? ' ext:qtip=&quot;' + item.tooltip + '&quot;' : '') + '&gt;' + (item.text||'') + '&lt;/a&gt;';
                    if (i &lt; l - 1) v += '&amp;nbsp;&amp;nbsp;&amp;nbsp;&amp;nbsp;';
                }
                return v;
            };
        },
    
        destroy: function() {
            delete this.items;
            delete this.renderer;
            return Ext.grid.LinkColumn.superclass.destroy.apply(this, arguments);
        },
    
        /**
         * @private
         * Process and refire events routed from the GridView's processEvent method.
         * Also fires any configured click handlers. By default, cancels the mousedown event to prevent selection.
         * Returns the event handler's status to allow cancelling of GridView's bubbling process.
         */
        processEvent : function(name, e, grid, rowIndex, colIndex){
            var m = e.getTarget().className.match(this.linkIdRe),
                item, fn;
            if (m &amp;&amp; (item = this.items[parseInt(m[1], 10)])) {
                if (name == 'click') {
                    (fn = item.handler || this.handler) &amp;&amp; fn.call(item.scope||this.scope||this, grid, rowIndex, colIndex, item, e);
                } else if ((name == 'mousedown') &amp;&amp; (item.stopSelection !== false)) {
                    return false;
                }
            }
            return Ext.grid.LinkColumn.superclass.processEvent.apply(this, arguments);
        }
    });
    
    //register ptype
    Ext.preg('linkcolumn', Ext.grid.LinkColumn);
    
    // register Column xtype
    Ext.grid.Column.types.linkcolumn = Ext.grid.LinkColumn;</p></div>
    ";i:2;s:1116:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="js" style="font-family:monospace;">    {
                xtype: 'linkcolumn',
                header: '操作',
                width: 100,
                sortable: true,
                items: [{
                    text: '查看',
                    handler: function(grid, rowIndex, colIndex) {
                        var record = grid.store.getAt(rowIndex);
                        new stat_task_his_win({
                            record: record
                        });
                    }
                }]
        }</pre></td></tr></table><p class="theCode" style="display:none;">    {
                xtype: 'linkcolumn',
                header: '操作',
                width: 100,
                sortable: true,
                items: [{
                    text: '查看',
                    handler: function(grid, rowIndex, colIndex) {
                        var record = grid.store.getAt(rowIndex);
                        new stat_task_his_win({
                            record: record
                        });
                    }
                }]
        }</p></div>
    ";}
categories:
  - 网页前端
tags:
  - extjs
  - grid
  - 按钮列
  - 链接按钮列

---
## 问题

想要在Extjs grid每一行添加一个链接或者添加一个按钮，怎么办？  
[<img class="alignnone size-full wp-image-963" title="extjs" src="http://fatkun.com/wp-content/uploads/2011/10/extjs.bmp" alt="" />][1]
## 解决方法

实现方法一是用renderer，但是这个链接的方法必须调用全局的变量。  
方法二就是我将要介绍的。
ActionColumn是显示一个图标按钮，而我需要一个链接按钮呢？改写ActionColumn代码即可。  
代码如下，主要是修改了renderer，如果你想改成button也是可以的：
<pre escaped="true" lang="js">/*!
 * Ext JS Library 3.3.1
 * Copyright(c) 2006-2010 Sencha Inc.
 * licensing@sencha.com
 * http://www.sencha.com/license
 */
Ext.grid.LinkColumn = Ext.extend(Ext.grid.Column, {
    header: '&#160;',
    linkIdRe: /x-link-col-(\d+)/,

    constructor: function(cfg) {
        var me = this,
            items = cfg.items || (me.items = [me]),
            l = items.length,
            i,
            item;

        Ext.grid.LinkColumn.superclass.constructor.call(me, cfg);

        me.renderer = function(v, meta) {
//          Allow a configured renderer to create initial value (And set the other values in the "metadata" argument!)
            v = Ext.isFunction(cfg.renderer) ? cfg.renderer.apply(this, arguments)||'' : '';

            meta.css += ' x-link-col-cell';
            for (i = 0; i &lt; l; i++) {
                item = items[i];
                v += '&lt;a href="javascript:;" class="x-link-col-icon x-link-col-' + String(i) + ' ' + (Ext.isFunction(item.getClass) ? item.getClass.apply(item.scope||this.scope||this, arguments) : '') + '"' +
                    ((item.tooltip) ? ' ext:qtip="' + item.tooltip + '"' : '') + '&gt;' + (item.text||'') + '&lt;/a&gt;';
                if (i &lt; l - 1) v += '&nbsp;&nbsp;&nbsp;&nbsp;';
            }
            return v;
        };
    },

    destroy: function() {
        delete this.items;
        delete this.renderer;
        return Ext.grid.LinkColumn.superclass.destroy.apply(this, arguments);
    },

    /**
     * @private
     * Process and refire events routed from the GridView's processEvent method.
     * Also fires any configured click handlers. By default, cancels the mousedown event to prevent selection.
     * Returns the event handler's status to allow cancelling of GridView's bubbling process.
     */
    processEvent : function(name, e, grid, rowIndex, colIndex){
        var m = e.getTarget().className.match(this.linkIdRe),
            item, fn;
        if (m && (item = this.items[parseInt(m[1], 10)])) {
            if (name == 'click') {
                (fn = item.handler || this.handler) && fn.call(item.scope||this.scope||this, grid, rowIndex, colIndex, item, e);
            } else if ((name == 'mousedown') && (item.stopSelection !== false)) {
                return false;
            }
        }
        return Ext.grid.LinkColumn.superclass.processEvent.apply(this, arguments);
    }
});

//register ptype
Ext.preg('linkcolumn', Ext.grid.LinkColumn);

// register Column xtype
Ext.grid.Column.types.linkcolumn = Ext.grid.LinkColumn;</pre>
## 使用方法

引用扩展的文件后，在grid columns加一个xtype: &#8216;linkcolumn&#8217;的列
<pre escaped="true" lang="js">{
            xtype: 'linkcolumn',
            header: '操作',
            width: 100,
            sortable: true,
            items: [{
                text: '查看',
                handler: function(grid, rowIndex, colIndex) {
                    var record = grid.store.getAt(rowIndex);
                    new stat_task_his_win({
                        record: record
                    });
                }
            }]
    }</pre>

 [1]: http://fatkun.com/wp-content/uploads/2011/10/extjs.bmp