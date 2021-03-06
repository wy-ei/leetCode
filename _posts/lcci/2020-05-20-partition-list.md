---
title: 分割链表
qid: 02.04
tags: [链表,双指针]
---


- 难度：Medium
- 题目链接：[https://leetcode-cn.com/problems/partition-list-lcci/](https://leetcode-cn.com/problems/partition-list-lcci/)


## 题目描述

来源于 [https://leetcode-cn.com/](https://leetcode-cn.com/)

<p>编写程序以 x 为基准分割链表，使得所有小于 x 的节点排在大于或等于 x 的节点之前。如果链表中包含 x，x 只需出现在小于 x 的元素之后(如下所示)。分割元素 x 只需处于&ldquo;右半部分&rdquo;即可，其不需要被置于左右两部分之间。</p>

<p><strong>示例:</strong></p>

<pre><strong>输入:</strong> head = 3-&gt;5-&gt;8-&gt;5-&gt;10-&gt;2-&gt;1, <em>x</em> = 5
<strong>输出:</strong> 3-&gt;1-&gt;2-&gt;10-&gt;5-&gt;5-&gt;8
</pre>


## 解法：

把链表分为两部分，值小于 x 的节点插入到 left 链表上，值不小于 x 的节点插入到 right 链表上，最后把两个链表连起来。

```c++
class Solution {
public:
    ListNode* partition(ListNode* head, int x) {
        ListNode left(0), right(0);
        ListNode *left_ptr = &left, *right_ptr = &right;

        for(ListNode *p = head; p != nullptr; p = p->next){
            if(p->val < x){
                left_ptr->next = p;
                left_ptr = p;
            }else{
                right_ptr->next = p;
                right_ptr = p;
            }
        }
        right_ptr->next = nullptr;
        left_ptr->next = right.next;
        return left.next;
    }
};
```