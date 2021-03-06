---
title: 最小差
qid: 16.06
tags: [数组,双指针]
---


- 难度：Medium
- 题目链接：[https://leetcode-cn.com/problems/smallest-difference-lcci/](https://leetcode-cn.com/problems/smallest-difference-lcci/)
- 标签：双指针

## 题目描述

来源于 [https://leetcode-cn.com/](https://leetcode-cn.com/)

<p>给定两个整数数组<code>a</code>和<code>b</code>，计算具有最小差绝对值的一对数值（每个数组中取一个值），并返回该对数值的差</p>
<p><strong>示例：</strong></p>
<pre><strong>输入：</strong>{1, 3, 15, 11, 2}, {23, 127, 235, 19, 8}
<strong>输出：</strong> 3，即数值对(11, 8)
</pre>
<p><strong>提示：</strong></p>
<ul>
<li><code>1 <= a.length, b.length <= 100000</code></li>
<li><code>-2147483648 <= a[i], b[i] <= 2147483647</code></li>
<li>正确结果在区间[-2147483648, 2147483647]内</li>
</ul>


## 解法：

先对数组排序，设置 `i = j = 0`，如果 `a[i] - b[j] < 0` 为了让两数之差接近 0，自然想要增大减数，因此 `i++`。反之，如果 `a[i] - b[j] > 0` 自然要扩大后者，因此 `j++`。

那么 `i++` 之后，i 前面的数有没有可能和 j 后面的某个数构成最小的差呢？不会的，`nums[i]` 前面的数比 `nums[i]` 更小， 减去一个比 `nums[j]` 更大的数，差只会更大。因此可以放心地排除 `i` 前面的数。

```c++
class Solution {
public:
    int smallestDifference(vector<int>& a, vector<int>& b) {
        sort(a.begin(), a.end());
        sort(b.begin(), b.end());

        long long min_diff = numeric_limits<long long>::max();
        int a_len = a.size(), b_len = b.size();
        int i = 0, j = 0;
        while(i < a_len && j < b_len){
            long long diff = static_cast<long long>(a[i]) - b[j];
            min_diff = min(min_diff, abs(diff));
            if(diff < 0){
                i++;
            }else{
                j++;
            }
        }
        return static_cast<int>(min_diff);
    }
};
```