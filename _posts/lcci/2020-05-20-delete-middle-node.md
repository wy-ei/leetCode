---
title: 删除中间节点
qid: 02.03
tags: [链表]
---


- 难度：Easy
- 题目链接：[https://leetcode-cn.com/problems/delete-middle-node-lcci/](https://leetcode-cn.com/problems/delete-middle-node-lcci/)


## 题目描述

来源于 [https://leetcode-cn.com/](https://leetcode-cn.com/)

<p>实现一种算法，删除单向链表中间的某个节点（即不是第一个或最后一个节点），假定你只能访问该节点。</p>



<p><strong>示例：</strong></p>

<pre><strong>输入：</strong>单向链表a-&gt;b-&gt;c-&gt;d-&gt;e-&gt;f中的节点c
<strong>结果：</strong>不返回任何数据，但该链表变为a-&gt;b-&gt;d-&gt;e-&gt;f
</pre>


## 解法：

```c++
class Solution {
public:
    void deleteNode(ListNode* node) {
        if(node == nullptr) return;
        if(node->next == nullptr){
            throw logic_error("can not delete last node");
        }
        node->val = node->next->val;
        node->next = node->next->next;
    }
};
```