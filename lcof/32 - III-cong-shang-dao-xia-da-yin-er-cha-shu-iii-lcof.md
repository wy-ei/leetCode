## 32 - III. 从上到下打印二叉树 III

- 难度：Medium
- 题目链接：[https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-iii-lcof/](https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-iii-lcof/)


## 题目描述

来源于 [https://leetcode-cn.com/](https://leetcode-cn.com/)

<p>请实现一个函数按照之字形顺序打印二叉树，即第一行按照从左到右的顺序打印，第二层按照从右到左的顺序打印，第三行再按照从左到右的顺序打印，其他行以此类推。</p>

<p>&nbsp;</p>

<p>例如:<br>
给定二叉树:&nbsp;<code>[3,9,20,null,null,15,7]</code>,</p>

<pre>    3
   / \
  9  20
    /  \
   15   7
</pre>

<p>返回其层次遍历结果：</p>

<pre>[
  [3],
  [20,9],
  [15,7]
]
</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ol>
	<li><code>节点总数 &lt;= 1000</code></li>
</ol>


## 解法：


记录一下当前层数，根据层数选择各层的方向即可。

```cpp
class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int>> ret;
        if(root == nullptr) return ret;

        int level = 0;
        queue<TreeNode*> node_queue;
        node_queue.push(root);

        while(!node_queue.empty()){
            vector<int> vec;
            int n = node_queue.size();
            for(int i=0;i<n;i++){
                TreeNode *node = node_queue.front();
                node_queue.pop();
                vec.push_back(node->val);
                if(node->left){
                    node_queue.push(node->left);
                }
                if(node->right){
                    node_queue.push(node->right);
                }
            }
            if(level % 2 == 0){
                ret.emplace_back(::move(vec));
            }else{
                ret.emplace_back(vec.rbegin(), vec.rend());
            }
            level++;
        }

        return ret;
    }
};
```