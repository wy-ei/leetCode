---
title: 递归乘法
qid: 08.05
tags: [递归]
---


- 难度：Medium
- 题目链接：[https://leetcode-cn.com/problems/recursive-mulitply-lcci/](https://leetcode-cn.com/problems/recursive-mulitply-lcci/)


## 题目描述

来源于 [https://leetcode-cn.com/](https://leetcode-cn.com/)

<p>递归乘法。 写一个递归函数，不使用 * 运算符， 实现两个正整数的相乘。可以使用加号、减号、位移，但要吝啬一些。</p>

<p> <strong>示例1:</strong></p>

<pre>
<strong> 输入</strong>：A = 1, B = 10
<strong> 输出</strong>：10
</pre>

<p> <strong>示例2:</strong></p>

<pre>
<strong> 输入</strong>：A = 3, B = 4
<strong> 输出</strong>：12
</pre>

<p> <strong>提示:</strong></p>

<ol>
<li>保证乘法范围不会溢出</li>
</ol>


## 解法：

计算 `A * B`，设 `B = 0b1011`，则 `A*B` 可以解释为： `A * 8 + A * 2 + A * 1`，这里只需要 `<<` 和 `+` 两种操作就够了。

```c++
class Solution {
public:
    int multiply(int A, int B) {
        int result = 0;
        int i = 0;
        while(B){
            if(B & 1){
                result += A << i;
            }
            B >>= 1;
            i++;
        }
        return result;
    }
};
```