---
title: 后继者
qid: 04.06
tags: [树,深度优先搜索]
---


- 难度：Medium
- 题目链接：[https://leetcode-cn.com/problems/successor-lcci/](https://leetcode-cn.com/problems/successor-lcci/)


## 题目描述

来源于 [https://leetcode-cn.com/](https://leetcode-cn.com/)

<p>设计一个算法，找出二叉搜索树中指定节点的&ldquo;下一个&rdquo;节点（也即中序后继）。</p>

<p>如果指定节点没有对应的&ldquo;下一个&rdquo;节点，则返回<code>null</code>。</p>

<p><strong>示例 1:</strong></p>

<pre><strong>输入:</strong> root = <code>[2,1,3], p = 1

  2
 / \
1   3
</code>
<strong>输出:</strong> 2</pre>

<p><strong>示例 2:</strong></p>

<pre><strong>输入:</strong> root = <code>[5,3,6,2,4,null,null,1], p = 6

      5
     / \
    3   6
   / \
  2   4
 /   
1
</code>
<strong>输出:</strong> null</pre>


## 解法：

中序遍历，寻找第一个值大于 p 的节点即可。

```c++
class Solution {
public:
    TreeNode* inorderSuccessor(TreeNode* root, TreeNode* p) {
        if(root == nullptr){
            return nullptr;
        }
        TreeNode* ret = inorderSuccessor(root->left, p);
        if(ret != nullptr){
            return ret;
        }
        if(root->val > p->val){
            return root;
        }
        return inorderSuccessor(root->right, p);
    }
};
```

中序遍历，保存前一个节点为 `prev`，当前节点为 `node`，当 `prev == p` 的时候，返回 `node` 节点。

```c++
class Solution {
public:
    TreeNode* inorderSuccessor(TreeNode* root, TreeNode* p) {
        if(traversal(root, p)){
            return prev;
        }
        return nullptr;
    }

    bool traversal(TreeNode* node, TreeNode* p){
        if(node == nullptr) return false;

        bool stop = traversal(node->left, p);
        if(stop){
            return true;
        }

        if(p == prev){
            prev = node;
            return true;
        }

        prev = node;

        stop = traversal(node->right, p);
        if(stop == true){
            return true;
        }

        return false;
    }
private:
    TreeNode* prev = nullptr;
};
```