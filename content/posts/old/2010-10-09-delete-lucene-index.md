---
title: 删除Lucene索引
author: fatkun
type: post
date: 2010-10-09T08:35:19+00:00
url: /2010/10/delete-lucene-index.html
duoshuo_thread_id:
  - 6300408770564457217
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:2301:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #003399;">String</span> indexDirStr <span style="color: #339933;">=</span> <span style="color: #0000ff;">&quot;d:<span style="color: #000099; font-weight: bold;">\\</span>index&quot;</span><span style="color: #339933;">;</span>
    Directory indexDir <span style="color: #339933;">=</span> FSDirectory.<span style="color: #006633;">getDirectory</span><span style="color: #009900;">&#40;</span><span style="color: #000000; font-weight: bold;">new</span> <span style="color: #003399;">File</span><span style="color: #009900;">&#40;</span>indexDirStr<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    IndexReader reader <span style="color: #339933;">=</span> IndexReader.<span style="color: #006633;">open</span><span style="color: #009900;">&#40;</span>indexDir<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    reader.<span style="color: #006633;">deleteDocuments</span><span style="color: #009900;">&#40;</span><span style="color: #000000; font-weight: bold;">new</span> Term<span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;id&quot;</span>, <span style="color: #003399;">String</span>.<span style="color: #006633;">valueOf</span><span style="color: #009900;">&#40;</span>id<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    reader.<span style="color: #006633;">flush</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    reader.<span style="color: #006633;">close</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span></pre></td></tr></table><p class="theCode" style="display:none;">String indexDirStr = &quot;d:\\index&quot;;
    Directory indexDir = FSDirectory.getDirectory(new File(indexDirStr));
    IndexReader reader = IndexReader.open(indexDir);
    reader.deleteDocuments(new Term(&quot;id&quot;, String.valueOf(id)));
    reader.flush();
    reader.close();</p></div>
    ";}
categories:
  - J2EE
tags:
  - Lucene
  - 删除索引

---
若需要从索引中删除某一个或者某一类文档，IndexReader提供了两种方法：
reader.DeleteDocument(int docNum)
reader.DeleteDocuments(Term term)。
前者是根据文档的编号来删除该文档，docNum是该文档进入索引时Lucene的编号，是按照顺序编的；后者是删除满足某一个条件的多个文档。
在执行了DeleteDocument或者DeleteDocuments方法后，系统会生成一个*.del的文件，该文件中记录了删除的文档，但并未从物理上删除这些文档。indexWriter.Optimize();才会真正的删除。
<pre escaped="true" lang="java">String indexDirStr = "d:\\index";
Directory indexDir = FSDirectory.getDirectory(new File(indexDirStr));
IndexReader reader = IndexReader.open(indexDir);
reader.deleteDocuments(new Term("id", String.valueOf(id)));
reader.flush();
reader.close();</pre>
注意new Term()中的id必须是Field.Index.TOKENIZED，不然无法搜索到就删除不了了。
另外注意一个问题是，我的lucene2.2版本删除后会在IndexReader.open时会出错！！换用新版的lucene2.9问题解决！