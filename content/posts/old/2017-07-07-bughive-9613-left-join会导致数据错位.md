---
title: '[BUG]HIVE-9613 left join会导致数据错位'
author: fatkun
type: post
date: 2017-07-07T10:32:00+00:00
url: /2017/07/bughive-9613-left-join会导致数据错位.html
categories:
  - hive
tags:
  - bug
  - hive

---
<table class="confluenceTable">  <tr>    <th class="confluenceTh">      category    </th>
    <th class="confluenceTh">      city    </th>
    <th class="confluenceTh">      rank    </th>
    <th class="confluenceTh">      src_category_en    </th>
    <th class="confluenceTh">      src_city_name_en    </th>  </tr>
  <tr>    <td class="confluenceTd">      jinrongfuwu    </td>
    <td class="confluenceTd">      shanghai    </td>
    <td class="confluenceTd">      1    </td>
    <td class="confluenceTd">      danbaobaoxiantouzi    </td>
    <td class="confluenceTd">      sh    </td>  </tr>
  <tr>    <td class="confluenceTd">      ktvjiuba    </td>
    <td class="confluenceTd">      shanghai    </td>
    <td class="confluenceTd">      2    </td>
    <td class="confluenceTd">      zpwentiyingshi    </td>
    <td class="confluenceTd">      sh    </td>  </tr></table>
but int hive0.14,the results in the column **src\_category\_en** is wrong,and is just the **city** contents:
<table class="confluenceTable">  <tr>    <th class="confluenceTh">      category    </th>
    <th class="confluenceTh">      city    </th>
    <th class="confluenceTh">      rank    </th>
    <th class="confluenceTh">      src_category_en    </th>
    <th class="confluenceTh">      src_city_name_en    </th>  </tr>
  <tr>    <td class="confluenceTd">      jinrongfuwu    </td>
    <td class="confluenceTd">      shanghai    </td>
    <td class="confluenceTd">      1    </td>
    <td class="confluenceTd">      shanghai    </td>
    <td class="confluenceTd">      sh    </td>  </tr>
  <tr>    <td class="confluenceTd">      ktvjiuba    </td>
    <td class="confluenceTd">      shanghai    </td>
    <td class="confluenceTd">      2    </td>
    <td class="confluenceTd">      shanghai    </td>
    <td class="confluenceTd">      sh    </td>  </tr></table>