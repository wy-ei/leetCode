---
title: 旋转矩阵
qid: 01.07
tags: [数组]
---


- 难度：Medium
- 题目链接：[https://leetcode-cn.com/problems/rotate-matrix-lcci/](https://leetcode-cn.com/problems/rotate-matrix-lcci/)


## 题目描述

来源于 [https://leetcode-cn.com/](https://leetcode-cn.com/)

<p>给你一幅由 <code>N &times; N</code> 矩阵表示的图像，其中每个像素的大小为 4 字节。请你设计一种算法，将图像旋转 90 度。</p>

<p>不占用额外内存空间能否做到？</p>



<p><strong>示例 1:</strong></p>

<pre>给定 <strong>matrix</strong> = 
[
  [1,2,3],
  [4,5,6],
  [7,8,9]
],

<strong>原地</strong>旋转输入矩阵，使其变为:
[
  [7,4,1],
  [8,5,2],
  [9,6,3]
]
</pre>

<p><strong>示例 2:</strong></p>

<pre>给定 <strong>matrix</strong> =
[
  [ 5, 1, 9,11],
  [ 2, 4, 8,10],
  [13, 3, 6, 7],
  [15,14,12,16]
], 

<strong>原地</strong>旋转输入矩阵，使其变为:
[
  [15,13, 2, 5],
  [14, 3, 4, 1],
  [12, 6, 8, 9],
  [16, 7,10,11]
]
</pre>


## 解法：

把矩阵的每一层做如下旋转：

![](https://wangyu-name.oss-cn-hangzhou.aliyuncs.com/superbed/2020/05/21/5ec664e3c2a9a83be5d2042e.jpg)

```c++
for(int i = 0; i < n; i++){
    t = top[i]
    top[i] = left[i]
    left[i] = bottom[i]
    bottom[i] = right[i]
    right[i] = t
}
```

只需要再使用一层循环来控制要旋转的层即可。


```c++
class Solution {
public:
    void rotate(vector<vector<int>>& matrix) {
        int N = matrix.size();
        for(int offset=0;offset<N/2;offset++){
            for(int j=offset;j<N-offset-1;j++){
                int num = matrix[offset][j];
                matrix[offset][j] = matrix[N-j-1][offset];
                matrix[N-j-1][offset] = matrix[N-offset-1][N-j-1];
                matrix[N-offset-1][N-j-1] = matrix[j][N-offset-1];
                matrix[j][N-offset-1] = num;
            }
        }
    }
};
```