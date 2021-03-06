---
title: 返回倒数第 k 个节点
qid: 02.02
tags: [链表,双指针]
dup: true
---


- 难度：Easy
- 题目链接：[https://leetcode-cn.com/problems/kth-node-from-end-of-list-lcci/](https://leetcode-cn.com/problems/kth-node-from-end-of-list-lcci/)


## 题目描述

来源于 [https://leetcode-cn.com/](https://leetcode-cn.com/)

<p>实现一种算法，找出单向链表中倒数第 k 个节点。返回该节点的值。</p>

<p><strong>注意：</strong>本题相对原题稍作改动</p>

<p><strong>示例：</strong></p>

<pre><strong>输入：</strong> 1-&gt;2-&gt;3-&gt;4-&gt;5 和 <em>k</em> = 2
<strong>输出： </strong>4</pre>

<p><strong>说明：</strong></p>

<p>给定的 <em>k</em>&nbsp;保证是有效的。</p>


## 解法一：快慢指针

```c++
class Solution {
public:
    int kthToLast(ListNode* head, int k) {
        ListNode *fast = head, *slow = head;
        for(int i=0;i<k;i++){
            fast = fast->next;
        }
        while(fast != nullptr){
            fast = fast->next;
            slow = slow->next;
        }
        return slow->val;
    }
};
```

## 解法二：递归

传入一个整型的指针或者引用，初始是值为 `k`，在递归退出的时候将其减 1，当递归退出到倒数第 k 个节点时，其值自然已经减小为 `0` 了，此时返回当前节点即可。

```c++
class Solution {
public:
    int kthToLast(ListNode* head, int k) {
        ListNode *node = kth_node_to_last(head, k);
        return node->val;
    }

private:
    static ListNode* kth_node_to_last(ListNode* head, int& k){
        if(head == nullptr) return nullptr;
        ListNode* node = kth_node_to_last(head->next, k);
        if(node != nullptr){
            return node;
        }
        
        k--;
        if(k == 0){
            return head;
        }
        
        return nullptr;
    }
};
```