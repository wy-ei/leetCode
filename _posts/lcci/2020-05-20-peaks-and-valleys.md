---
title: 峰与谷
qid: 10.11
---


- 难度：Medium
- 题目链接：[https://leetcode-cn.com/problems/peaks-and-valleys-lcci/](https://leetcode-cn.com/problems/peaks-and-valleys-lcci/)


## 题目描述

来源于 [https://leetcode-cn.com/](https://leetcode-cn.com/)

<p>在一个整数数组中，&ldquo;峰&rdquo;是大于或等于相邻整数的元素，相应地，&ldquo;谷&rdquo;是小于或等于相邻整数的元素。例如，在数组{5, 8, 6, 2, 3, 4, 6}中，{8, 6}是峰， {5, 2}是谷。现在给定一个整数数组，将该数组按峰与谷的交替顺序排序。</p>

<p><strong>示例:</strong></p>

<pre><strong>输入: </strong>[5, 3, 1, 2, 3]
<strong>输出:</strong>&nbsp;[5, 1, 3, 2, 3]
</pre>

<p><strong>提示：</strong></p>

<ul>
	<li><code>nums.length &lt;= 10000</code></li>
</ul>


## 解法：

希望谷峰交错，即在整个序列中，前一个数减去后一个数，要正负交替。

假如希望先出现峰，那么需要 `nums[0] > nums[1]`，否则交换两者即可。接下来需要一个谷，需要 `nums[1] < nums[2]`，如果 `nums[2] < nums[1]`，那么交换后 `nums[0]` 必然还是大于 `nums[1]` 的。因此，交换后不会影响前面。

```c++
class Solution {
public:
    void wiggleSort(vector<int>& nums) {
        int sign = 1;
        for(int i=1;i<nums.size();i++){
            if((nums[i-1] - nums[i]) * sign < 0){
                ::swap(nums[i], nums[i-1]);
            }
            sign *= -1;
        }
    }
};
```