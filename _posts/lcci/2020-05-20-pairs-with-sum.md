---
title: 数对和
qid: 16.24
tags: [数组,哈希表]
---


- 难度：Medium
- 题目链接：[https://leetcode-cn.com/problems/pairs-with-sum-lcci/](https://leetcode-cn.com/problems/pairs-with-sum-lcci/)


## 题目描述

来源于 [https://leetcode-cn.com/](https://leetcode-cn.com/)

<p>设计一个算法，找出数组中两数之和为指定值的所有整数对。一个数只能属于一个数对。</p>

<p><strong>示例 1:</strong></p>

<pre><strong>输入:</strong> nums = [5,6,5], target = 11
<strong>输出: </strong>[[5,6]]</pre>

<p><strong>示例 2:</strong></p>

<pre><strong>输入:</strong> nums = [5,6,5,6], target = 11
<strong>输出: </strong>[[5,6],[5,6]]</pre>

<p><strong>提示：</strong></p>

<ul>
	<li><code>nums.length &lt;= 100000</code></li>
</ul>


## 解法：

和 twosum 类似的思路。

```c++
class Solution {
public:
    vector<vector<int>> pairSums(vector<int>& nums, int target) {
        vector<vector<int>> ret;
        unordered_map<int, int> num_to_count;
        for(int num: nums){
            int other = target - num;
            if(num_to_count.find(other) != num_to_count.end() && num_to_count[other] > 0){
                ret.emplace_back(vector<int>({num, target-num}));
                num_to_count[other]--;
            }else{
                num_to_count[num]++;
            }
        }
        return ret;
    }
};
```