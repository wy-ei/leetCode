---
title: 检查子树
qid: 04.10
tags: [树]
---


- 难度：Medium
- 题目链接：[https://leetcode-cn.com/problems/check-subtree-lcci/](https://leetcode-cn.com/problems/check-subtree-lcci/)


## 题目描述

来源于 [https://leetcode-cn.com/](https://leetcode-cn.com/)

<p>检查子树。你有两棵非常大的二叉树：T1，有几万个节点；T2，有几万个节点。设计一个算法，判断 T2 是否为 T1 的子树。</p>

<p>如果 T1 有这么一个节点 n，其子树与 T2 一模一样，则 T2 为 T1 的子树，也就是说，从节点 n 处把树砍断，得到的树与 T2 完全相同。</p>

<p><strong>示例1:</strong></p>

<pre><strong> 输入</strong>：t1 = [1, 2, 3], t2 = [2]
<strong> 输出</strong>：true
</pre>

<p><strong>示例2:</strong></p>

<pre><strong> 输入</strong>：t1 = [1, null, 2, 4], t2 = [3, 2]
<strong> 输出</strong>：false
</pre>

<p><strong>提示：</strong></p>

<ol>
	<li>树的节点数目范围为[0, 20000]。</li>
</ol>


## 解法：

先计算出 T2 的高度 h2，然后以 t1 中高度为 h2 的节点为根节点，判断是否与 T2 相同。

```c++
class Solution {
public:
    bool checkSubTree(TreeNode* t1, TreeNode* t2) {
        int t2_height = tree_height(t2);
        
        bool has_sub_tree = false;
        auto func = [&has_sub_tree,&t2,this](TreeNode* node){
            if(has_sub_tree){
                return;
            }
            if(is_equal_tree(node, t2)){
                has_sub_tree = true;
            }
        };

        run_at_height(t1, t2_height, func);

        return has_sub_tree;
    }

private:
    int run_at_height(TreeNode *node, int height, const function<void(TreeNode* node)> &func){
        if(node == nullptr) return 0;
        int left_height = run_at_height(node->left, height, func);
        int right_height = run_at_height(node->right, height, func);
        int h = 1 + max(left_height, right_height);
        if(height == h){
            func(node);
        }
        return h;
    }
    
    int tree_height(TreeNode *node){
        if(node == nullptr) return 0;
        return 1 + max(tree_height(node->left), tree_height(node->right));
    }

    bool is_equal_tree(TreeNode* t1, TreeNode* t2){
        if(!t1 && !t2) return true;
        if(!t1 || !t2) return false;
        if(t1->val != t2->val) return false;
        return is_equal_tree(t1->left, t2->left) &&
               is_equal_tree(t1->right, t2->right);
    }
};
```