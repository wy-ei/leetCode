---
title: 合并排序的数组
qid: 10.01
tags: [数组,双指针]
---


- 难度：Easy
- 题目链接：[https://leetcode-cn.com/problems/sorted-merge-lcci/](https://leetcode-cn.com/problems/sorted-merge-lcci/)


## 题目描述

来源于 [https://leetcode-cn.com/](https://leetcode-cn.com/)

<p>给定两个排序后的数组 A 和 B，其中 A 的末端有足够的缓冲空间容纳 B。 编写一个方法，将 B 合并入 A 并排序。</p>

<p>初始化&nbsp;A 和 B 的元素数量分别为&nbsp;<em>m</em> 和 <em>n</em>。</p>

<p><strong>示例:</strong></p>

<pre><strong>输入:</strong>
A = [1,2,3,0,0,0], m = 3
B = [2,5,6],       n = 3

<strong>输出:</strong>&nbsp;[1,2,2,3,5,6]</pre>

<p><strong>说明:</strong></p>

<ul>
	<li><code>A.length == n + m</code></li>
</ul>


## 解法：

从后面开始归并即可。

```c++
class Solution {
public:
    void merge(vector<int>& A, int m, vector<int>& B, int n) {
        int i = m - 1;
        int j = n - 1;
        int k = m + n - 1;
        while(i >= 0 || j >= 0){
            if(i == -1){
                A[k--] = B[j--];
            }else if(j == -1){
                A[k--] = A[i--];
            }else if(A[i] <= B[j]){
                A[k--] = B[j--];
            }else{
                A[k--] = A[i--];
            }
        }
    }
};
```