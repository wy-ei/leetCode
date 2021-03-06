---
title: 检查平衡性
qid: 04.04
tags: [树,深度优先搜索]
dup: true
---


- 难度：Easy
- 题目链接：[https://leetcode-cn.com/problems/check-balance-lcci/](https://leetcode-cn.com/problems/check-balance-lcci/)


## 题目描述

来源于 [https://leetcode-cn.com/](https://leetcode-cn.com/)

<p>实现一个函数，检查二叉树是否平衡。在这个问题中，平衡树的定义如下：任意一个节点，其两棵子树的高度差不超过 1。</p><br><strong>示例 1:</strong><pre>给定二叉树 [3,9,20,null,null,15,7]<br>    3<br>   / &#92<br>  9  20<br>    /  &#92<br>   15   7<br>返回 true 。</pre><strong>示例 2:</strong><br><pre>给定二叉树 [1,2,2,3,3,null,null,4,4]<br>      1<br>     / &#92<br>    2   2<br>   / &#92<br>  3   3<br> / &#92<br>4   4<br>返回 false 。</pre>

## 解法：

递归地计算左右子树的深度，发现不平衡后，抛出异常，由此立刻退出递归调用。

```c++
class Solution {
public:
    bool isBalanced(TreeNode* root) {
        try{
            throw_if_unbalance(root);
            return true;
        }catch(...){
            return false;
        }
    }
private:
    int throw_if_unbalance(TreeNode* node) {
        if(node == nullptr){
            return 0;
        }

        int left_depth = throw_if_unbalance(node->left);
        int right_depth = throw_if_unbalance(node->right);

        if(abs(left_depth - right_depth) > 1){
            throw exception();
        }
        return 1 + max(left_depth, right_depth);
    }
};
```