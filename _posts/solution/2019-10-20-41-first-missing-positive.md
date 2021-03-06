---
title: 缺失的第一个正数
qid: 41
tags: [数组]
---


- 难度： 困难
- 通过率： 27.7%
- 题目链接：[https://leetcode-cn.com/problems/first-missing-positive](https://leetcode-cn.com/problems/first-missing-positive)


## 题目描述

来源于 [https://leetcode-cn.com/](https://leetcode-cn.com/)

<p>给定一个未排序的整数数组，找出其中没有出现的最小的正整数。</p>

<p><strong>示例&nbsp;1:</strong></p>

<pre>输入: [1,2,0]
输出: 3
</pre>

<p><strong>示例&nbsp;2:</strong></p>

<pre>输入: [3,4,-1,1]
输出: 2
</pre>

<p><strong>示例&nbsp;3:</strong></p>

<pre>输入: [7,8,9,11,12]
输出: 1
</pre>

<p><strong>说明:</strong></p>

<p>你的算法的时间复杂度应为O(<em>n</em>)，并且只能使用常数级别的空间。</p>


## 解法：

如果数组中出现了 `n`，且 `0 < n < nums.size()`，那么就在 `nums[n]` 中记录该值出现过。但是 `nums[n]` 中的值在后面遍历的时候还需要使用。如何在保存原有信息的同时在 `nums[n]` 中记录下 `n` 出现过，这是关键。

如果数组中的数全部为正，那么可以设置 `nums[n] = -nums[n]`，即如果 `nums[n]` 是负的，说明 `n` 存在在原数组中。遍历的时候遇到负值，可以通过取反的得到原来的数。但这里输入数组存在负值，可以先遍历数组把负数修改为 `INT_MAX`。

遍历完成后，数组中第一个大于 0 的数的下标，就是要找的数。因为长度为 `m` 的数组中，最大下标是 `m-1`，如果数组中存放的是 `1~m`，那么 `m` 就无法标记。因此，我们使用下标 `0` 来标记 `1`。 

```c++
class Solution {
public:
    int firstMissingPositive(vector<int>& nums) {
        if(nums.empty()){
            return 1;
        }
        const int MAX_INT = numeric_limits<int>::max();
        transform(nums.begin(), nums.end(), nums.begin(), [MAX_INT](int n){
            return (n <= 0) ? MAX_INT : n;
        });

        for(int n: nums){
            if(n < 0){
                n = -n;
            }
            if(n > nums.size()) {
                continue;
            }
            if(nums[n-1] > 0){
                nums[n-1] = -nums[n-1];
            }
        }
        
        for(size_t i=0;i<nums.size();i++){
            if(nums[i] > 0){
                return i + 1;
            }
        }
        return nums.size() + 1;
    }
};
```