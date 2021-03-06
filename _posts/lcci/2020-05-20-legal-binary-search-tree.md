---
title: 合法二叉搜索树
qid: 04.05
tags: [树,深度优先搜索]
---


- 难度：Medium
- 题目链接：[https://leetcode-cn.com/problems/legal-binary-search-tree-lcci/](https://leetcode-cn.com/problems/legal-binary-search-tree-lcci/)


## 题目描述

来源于 [https://leetcode-cn.com/](https://leetcode-cn.com/)

<p>实现一个函数，检查一棵二叉树是否为二叉搜索树。</p><strong>示例 1:</strong><pre><strong>输入:</strong><br>    2<br>   / &#92<br>  1   3<br><strong>输出:</strong> true<br></pre><strong>示例 2:</strong><pre><strong>输入:</strong><br>    5<br>   / &#92<br>  1   4<br>     / &#92<br>    3   6<br><strong>输出:</strong> false<br><strong>解释:</strong> 输入为: [5,1,4,null,null,3,6]。<br>     根节点的值为 5 ，但是其右子节点值为 4 。</pre>

## 解法：

对于每个节点，它的值都有一个合法的范围，可以递归地检查每个节点是否符合要求。由于二叉树中的可能存在 `MAX_INT` 和 `MIN_INT`，因此使用 64 位整型来比较。

```c++
class Solution {
public:
    bool isValidBST(TreeNode* root) {
        return isValidBST(root, numeric_limits<int64_t>::min(), numeric_limits<int64_t>::max());
    }

    bool isValidBST(TreeNode* root, int64_t lo, int64_t hi){
        if(root == nullptr) return true;
        int64_t val = root->val;
        if(val >= hi) return false;
        if(val <= lo) return false;
        return isValidBST(root->left, lo, root->val)
            && isValidBST(root->right, root->val, hi);
    }
};
```

由于二叉搜索的先序遍历序列是严格递增的，因此可以先序遍历二叉搜索树，检查每个节点的值是否严格递增。

```c++
class Solution {
public:
    bool isValidBST(TreeNode* root) {
        int64_t prev = numeric_limits<int64_t>::min();
        return traversal(root, &prev);
    }

    bool traversal(TreeNode* node, int64_t *prev){
        if(node == nullptr) return true;
        bool ret = traversal(node->left, prev);
        if(ret == false){
            return false;
        }

        if(*prev >= node->val){
            return false;
        }
        *prev = node->val;

        ret = traversal(node->right, prev);
        if(ret == false){
            return false;
        }
        return true;
    }
};
```