---
title: Extjs3 PagingToolbar下拉框分页插件
author: fatkun
type: post
date: 2012-03-11T17:37:40+00:00
url: /2012/03/extjs3-pagingtoolbar-combbox.html
duoshuo_thread_id:
  - 6300408840642888450
wp-syntax-cache-content:
  - |
    a:2:{i:1;s:6728:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="js" style="font-family:monospace;">Ext.namespace('Ext.ui.plugins');
    &nbsp;
     Ext.ui.plugins.ComboPageSize = function(config) {
         Ext.apply(this, config);
     };
    &nbsp;
     Ext.extend(Ext.ui.plugins.ComboPageSize, Ext.util.Observable, {
    &nbsp;
         pageSizes: [25, 50, 100, 200, 500],
         prefixText: '每页显示',
         postfixText: '条',
         addToItem: true,    //true添加到items中去，配合index；false则直接添加到最后
         index: 10,           //在items中的位置
         init: function(pagingToolbar) {
             var ps = this.pageSizes;
             var combo = new Ext.form.ComboBox({
                 typeAhead: true,
                 triggerAction: 'all',
                 lazyRender: true,
                 mode: 'local',
                 width: 80,
                 store: ps,
                 enableKeyEvents: true,
                 editable: false,
                 loadPages: function() {
                     var rowIndex = 0;
                     var gp = pagingToolbar.findParentBy(
                                     function(ct, cmp) { return (ct instanceof Ext.grid.GridPanel) ? true : false; }
                                   );
                     var sm = gp.getSelectionModel();
                     if (undefined != sm &amp;&amp; sm.hasSelection()) {
                         if (sm instanceof Ext.grid.RowSelectionModel) {
                             rowIndex = gp.store.indexOf(sm.getSelected());
                         } else if (sm instanceof Ext.grid.CellSelectionModel) {
                             rowIndex = sm.getSelectedCell()[0];
                         }
                     }
                     rowIndex += pagingToolbar.cursor;
                     pagingToolbar.doLoad(Math.floor(rowIndex / pagingToolbar.pageSize) * pagingToolbar.pageSize);
                 },
                 listeners: {
                     select: function(c, r, i) {
                         pagingToolbar.pageSize = ps[i];
                         this.loadPages();
                     },
                     blur: function() {
                         var pagesizeTemp = Number(this.getValue());
                         if (isNaN(pagesizeTemp)) {
                             this.setValue(pagingToolbar.pageSize);
                             return;
                         }
                         pagingToolbar.pageSize = Number(this.getValue());
                         this.loadPages();
                     }
                 }
             });
             if (this.addToItem) {
                 var inputIndex = this.index;
                 if (inputIndex &gt; pagingToolbar.items.length) inputIndex = pagingToolbar.items.length;
                 pagingToolbar.insert(++inputIndex, '-');
                 pagingToolbar.insert(++inputIndex, this.prefixText);
                 pagingToolbar.insert(++inputIndex, combo);
                 pagingToolbar.insert(++inputIndex, this.postfixText);
             }
             else {
                 pagingToolbar.add('-');
                 pagingToolbar.add(this.prefixText);
                 pagingToolbar.add(combo);
                 pagingToolbar.add(this.postfixText);
             }
             pagingToolbar.on({
                 beforedestroy: function() {
                     combo.destroy();
                 },
                 change: function() {
                     combo.setValue(pagingToolbar.pageSize);
    &nbsp;
                 }
             });
    &nbsp;
         }
     })</pre></td></tr></table><p class="theCode" style="display:none;">Ext.namespace('Ext.ui.plugins');
     
     Ext.ui.plugins.ComboPageSize = function(config) {
         Ext.apply(this, config);
     };
     
     Ext.extend(Ext.ui.plugins.ComboPageSize, Ext.util.Observable, {
     
         pageSizes: [25, 50, 100, 200, 500],
         prefixText: '每页显示',
         postfixText: '条',
         addToItem: true,    //true添加到items中去，配合index；false则直接添加到最后
         index: 10,           //在items中的位置
         init: function(pagingToolbar) {
             var ps = this.pageSizes;
             var combo = new Ext.form.ComboBox({
                 typeAhead: true,
                 triggerAction: 'all',
                 lazyRender: true,
                 mode: 'local',
                 width: 80,
                 store: ps,
                 enableKeyEvents: true,
                 editable: false,
                 loadPages: function() {
                     var rowIndex = 0;
                     var gp = pagingToolbar.findParentBy(
                                     function(ct, cmp) { return (ct instanceof Ext.grid.GridPanel) ? true : false; }
                                   );
                     var sm = gp.getSelectionModel();
                     if (undefined != sm &amp;&amp; sm.hasSelection()) {
                         if (sm instanceof Ext.grid.RowSelectionModel) {
                             rowIndex = gp.store.indexOf(sm.getSelected());
                         } else if (sm instanceof Ext.grid.CellSelectionModel) {
                             rowIndex = sm.getSelectedCell()[0];
                         }
                     }
                     rowIndex += pagingToolbar.cursor;
                     pagingToolbar.doLoad(Math.floor(rowIndex / pagingToolbar.pageSize) * pagingToolbar.pageSize);
                 },
                 listeners: {
                     select: function(c, r, i) {
                         pagingToolbar.pageSize = ps[i];
                         this.loadPages();
                     },
                     blur: function() {
                         var pagesizeTemp = Number(this.getValue());
                         if (isNaN(pagesizeTemp)) {
                             this.setValue(pagingToolbar.pageSize);
                             return;
                         }
                         pagingToolbar.pageSize = Number(this.getValue());
                         this.loadPages();
                     }
                 }
             });
             if (this.addToItem) {
                 var inputIndex = this.index;
                 if (inputIndex &gt; pagingToolbar.items.length) inputIndex = pagingToolbar.items.length;
                 pagingToolbar.insert(++inputIndex, '-');
                 pagingToolbar.insert(++inputIndex, this.prefixText);
                 pagingToolbar.insert(++inputIndex, combo);
                 pagingToolbar.insert(++inputIndex, this.postfixText);
             }
             else {
                 pagingToolbar.add('-');
                 pagingToolbar.add(this.prefixText);
                 pagingToolbar.add(combo);
                 pagingToolbar.add(this.postfixText);
             }
             pagingToolbar.on({
                 beforedestroy: function() {
                     combo.destroy();
                 },
                 change: function() {
                     combo.setValue(pagingToolbar.pageSize);
     
                 }
             });
     
         }
     })</p></div>
    ";i:2;s:1018:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="js" style="font-family:monospace;">                bbar: new Ext.PagingToolbar({
                        plugins: new Ext.ui.plugins.ComboPageSize(),
                        pageSize: myPageSize,
                        displayInfo : true,
                        displayMsg : '当前记录数: {0} - {1} 总记录数: {2}',   
                        emptyMsg : '没有符合条件的记录',   
                        store : config.store
                    })</pre></td></tr></table><p class="theCode" style="display:none;">                bbar: new Ext.PagingToolbar({
                        plugins: new Ext.ui.plugins.ComboPageSize(),
                        pageSize: myPageSize,
                        displayInfo : true,
                        displayMsg : '当前记录数: {0} - {1} 总记录数: {2}',   
                        emptyMsg : '没有符合条件的记录',   
                        store : config.store
                    })</p></div>
    ";}
categories:
  - 网页前端
tags:
  - combbox
  - extjs
  - paging
  - 分页

---
Extjs PagingToolbar下拉框分页插件
<pre escaped="true" lang="js">Ext.namespace('Ext.ui.plugins');
 
 Ext.ui.plugins.ComboPageSize = function(config) {
     Ext.apply(this, config);
 };
 
 Ext.extend(Ext.ui.plugins.ComboPageSize, Ext.util.Observable, {
 
     pageSizes: [25, 50, 100, 200, 500],
     prefixText: '每页显示',
     postfixText: '条',
     addToItem: true,    //true添加到items中去，配合index；false则直接添加到最后
     index: 10,           //在items中的位置
     init: function(pagingToolbar) {
         var ps = this.pageSizes;
         var combo = new Ext.form.ComboBox({
             typeAhead: true,
             triggerAction: 'all',
             lazyRender: true,
             mode: 'local',
             width: 80,
             store: ps,
             enableKeyEvents: true,
             editable: false,
             loadPages: function() {
                 var rowIndex = 0;
                 var gp = pagingToolbar.findParentBy(
                                 function(ct, cmp) { return (ct instanceof Ext.grid.GridPanel) ? true : false; }
                               );
                 var sm = gp.getSelectionModel();
                 if (undefined != sm && sm.hasSelection()) {
                     if (sm instanceof Ext.grid.RowSelectionModel) {
                         rowIndex = gp.store.indexOf(sm.getSelected());
                     } else if (sm instanceof Ext.grid.CellSelectionModel) {
                         rowIndex = sm.getSelectedCell()[0];
                     }
                 }
                 rowIndex += pagingToolbar.cursor;
                 pagingToolbar.doLoad(Math.floor(rowIndex / pagingToolbar.pageSize) * pagingToolbar.pageSize);
             },
             listeners: {
                 select: function(c, r, i) {
                     pagingToolbar.pageSize = ps[i];
                     this.loadPages();
                 },
                 blur: function() {
                     var pagesizeTemp = Number(this.getValue());
                     if (isNaN(pagesizeTemp)) {
                         this.setValue(pagingToolbar.pageSize);
                         return;
                     }
                     pagingToolbar.pageSize = Number(this.getValue());
                     this.loadPages();
                 }
             }
         });
         if (this.addToItem) {
             var inputIndex = this.index;
             if (inputIndex &gt; pagingToolbar.items.length) inputIndex = pagingToolbar.items.length;
             pagingToolbar.insert(++inputIndex, '-');
             pagingToolbar.insert(++inputIndex, this.prefixText);
             pagingToolbar.insert(++inputIndex, combo);
             pagingToolbar.insert(++inputIndex, this.postfixText);
         }
         else {
             pagingToolbar.add('-');
             pagingToolbar.add(this.prefixText);
             pagingToolbar.add(combo);
             pagingToolbar.add(this.postfixText);
         }
         pagingToolbar.on({
             beforedestroy: function() {
                 combo.destroy();
             },
             change: function() {
                 combo.setValue(pagingToolbar.pageSize);
 
             }
         });
 
     }
 })
</pre>
## 使用方法

<pre escaped="true" lang="js">bbar: new Ext.PagingToolbar({
                    plugins: new Ext.ui.plugins.ComboPageSize(),
                    pageSize: myPageSize,
                    displayInfo : true,
                    displayMsg : '当前记录数: {0} - {1} 总记录数: {2}',   
                    emptyMsg : '没有符合条件的记录',   
                    store : config.store
                })</pre>
来源：<a href="http://www.cnblogs.com/badwps/archive/2011/04/15/2016440.html" title="Ext.PagingToolbar设置每页显示条数插件" target="_blank">Ext.PagingToolbar设置每页显示条数插件</a>  
作者还有个滑动条改变分页的，赞，链接过去看吧。