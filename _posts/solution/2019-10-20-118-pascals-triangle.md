---
title: 杨辉三角
qid: 118
tags: [数组]
---


- 难度： 简单
- 通过率： 43.5%
- 题目链接：[https://leetcode-cn.com/problems/pascals-triangle](https://leetcode-cn.com/problems/pascals-triangle)


## 题目描述

来源于 [https://leetcode-cn.com/](https://leetcode-cn.com/)

<p>给定一个非负整数&nbsp;<em>numRows，</em>生成杨辉三角的前&nbsp;<em>numRows&nbsp;</em>行。</p>

<p><img alt="" src="https://upload.wikimedia.org/wikipedia/commons/0/0d/PascalTriangleAnimated2.gif"></p>

<p><small>在杨辉三角中，每个数是它左上方和右上方的数的和。</small></p>

<p><strong>示例:</strong></p>

<pre><strong>输入:</strong> 5
<strong>输出:</strong>
[
     [1],
    [1,1],
   [1,2,1],
  [1,3,3,1],
 [1,4,6,4,1]
]</pre>


## 解法：

仿佛回到了大学一年级。

```python
class Solution:
    def generate(self, n_rows: int) -> List[List[int]]:
        triangle = []
        last_row = []
        
        for i_row in range(n_rows):
            row_len = i_row + 1
            row = [1] * row_len
            for i in range(1, row_len - 1):
                row[i] = last_row[i-1] + last_row[i]
            triangle.append(row)
            last_row = row

        return triangle
```