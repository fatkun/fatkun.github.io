---
title: 二叉树遍历（先序，中序，后序）
author: fatkun
type: post
date: 2010-11-24T11:31:08+00:00
url: /2010/11/binary-tree-traversal.html
duoshuo_thread_id:
  - 6300408787819823873
categories:
  - 胡言乱语
tags:
  - 二叉树

---
先序遍历：根结点-》左节点-》右节点  
中序遍历：左节点-》根结点-》右节点  
后续遍历：左节点-》右节点-》根结点  
![][1]  
上图的先序遍历为：ABDECF  
中序遍历：DBEAFC  
后序遍历：DEBFCA
原文来自[百度百科][2]
[代码可以看这里][3]，结合代码看算法更容易理解。
当你知道先序和中序时，要推出后序。 还是这道题，可以根据先序序列知道根节点是A，则可以知道DBE在左子树，FC在右子树。

 [1]: http://wah88w.blu.livefilestore.com/y1p2Ldn6_KhW1NuY9TuY8eX71yxR7bPzGcORcwu4Bu2rzNo4DycZl6MgOcQE2xYEGfW0fuOndYKyJrm2cdR0DwxD45hybQW6CA1/2x.png?psid=1
 [2]: http://baike.baidu.com/view/1455146.htm
 [3]: http://www.cppblog.com/ngaut/archive/2006/01/01/2351.aspx