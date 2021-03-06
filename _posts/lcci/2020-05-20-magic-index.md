---
title: 魔术索引
qid: 08.03
tags: [数组,二分查找]
---


- 难度：Easy
- 题目链接：[https://leetcode-cn.com/problems/magic-index-lcci/](https://leetcode-cn.com/problems/magic-index-lcci/)


## 题目描述

来源于 [https://leetcode-cn.com/](https://leetcode-cn.com/)

<p>魔术索引。 在数组<code>A[0...n-1]</code>中，有所谓的魔术索引，满足条件<code>A[i] = i</code>。给定一个有序整数数组，编写一种方法找出魔术索引，若有的话，在数组A中找出一个魔术索引，如果没有，则返回-1。若有多个魔术索引，返回索引值最小的一个。</p>

<p><strong>示例1:</strong></p>

<pre><strong> 输入</strong>：nums = [0, 2, 3, 4, 5]
<strong> 输出</strong>：0
<strong> 说明</strong>: 0下标的元素为0
</pre>

<p><strong>示例2:</strong></p>

<pre><strong> 输入</strong>：nums = [1, 1, 1]
<strong> 输出</strong>：1
</pre>

<p><strong>提示:</strong></p>

<ol>
	<li>nums长度在[1, 1000000]之间</li>
</ol>


## 解法：

在数组 `nums` 中不存在重复元素的情况下，如果 `mid < nums[mid]`，那么 mid 每增加 1，`nums[mid]` 后面的数也至少增加 1，因此 mid 之后的不可能存在 `i == nums[i]`，因此需要在 mid 之前寻找。

如果 `mid > nums[mid]`，那么 mid 每减小 1，`nums[mid]` 前面的数也至少减小 1，不可能出现 `i == nums[i]`，因此只能在 mid 之后寻找。

```c++
class Solution {
public:
    int findMagicIndex(vector<int>& nums) {
        return find(nums, 0, nums.size());
    }
private:
    int find(vector<int>& nums, int lo, int hi){

        while(lo < hi){
            int mid = lo + (hi - lo) / 2;
            if(mid < nums[mid]){
                return find(nums, lo, mid);
            }else if(mid > nums[mid]){
                return find(nums, mid+1, hi);
            }else{
                return mid;
            }
        }
        return -1;
    }
};
```

leetcode 上的测试用例中包含重复的元素，这与原书中的意思不同。上面代码无法通过 leetcode 的测试。