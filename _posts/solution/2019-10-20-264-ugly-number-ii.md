---
title: 丑数 II
qid: 264
tag: [堆, 数学, 动态规划]
---

- 难度： 中等
- 通过率： 35.0%
- 题目链接：[https://leetcode-cn.com/problems/ugly-number-ii](https://leetcode-cn.com/problems/ugly-number-ii)


## 题目描述

来源于 [https://leetcode-cn.com/](https://leetcode-cn.com/)

<p>编写一个程序，找出第 <code>n</code> 个丑数。</p>

<p>丑数就是只包含质因数&nbsp;<code>2, 3, 5</code> 的<strong>正整数</strong>。</p>

<p><strong>示例:</strong></p>

<pre><strong>输入:</strong> n = 10
<strong>输出:</strong> 12
<strong>解释: </strong><code>1, 2, 3, 4, 5, 6, 8, 9, 10, 12</code> 是前 10 个丑数。</pre>

<p><strong>说明:&nbsp;</strong>&nbsp;</p>

<ol>
	<li><code>1</code>&nbsp;是丑数。</li>
	<li><code>n</code>&nbsp;<strong>不超过</strong>1690。</li>
</ol>

## 解法：

新的丑数，肯定之前某个较小的丑数乘以 2、3、5 中的一个得到的。初始阶段这个较小的丑数就是 `1`。`1` 分别乘以 2、3、5 可以得到 3 个丑数。因此，这个较小的丑数可以乘以不同的因子产生多个新的丑数。一旦乘以 2 产生了新的丑数后，下一个通过与 2 相乘产生丑数的哪一个较小的数，一定是 1 后面的丑数。所以使用 3 个指针分别指向有可能通过与 2、3、5 相乘产生新的丑数的那个较小的数。一旦某个指针指向的数乘以对应的因子，产生了下一个丑数。那就把指针向后挪。

```c++
class Solution {
public:
    int nthUglyNumber(int index) {
        if(index < 1) return 0;
        vector<int> nums(index);
        nums[0] = 1;
        int i2 = 0, i3 = 0, i5 = 0;
        for(int i=1;i<index;i++){
            nums[i] = min({nums[i2]*2, nums[i3]*3, nums[i5]*5});
            if(nums[i] == nums[i2]*2) i2++;
            if(nums[i] == nums[i3]*3) i3++;
            if(nums[i] == nums[i5]*5) i5++;
        }
        return nums.back();
    }
};
```