---
title: 整数转换
qid: 05.06
tags: [位运算]
---


- 难度：Easy
- 题目链接：[https://leetcode-cn.com/problems/convert-integer-lcci/](https://leetcode-cn.com/problems/convert-integer-lcci/)


## 题目描述

来源于 [https://leetcode-cn.com/](https://leetcode-cn.com/)

<p>整数转换。编写一个函数，确定需要改变几个位才能将整数A转成整数B。</p>

<p> <strong>示例1:</strong></p>

<pre>
<strong> 输入</strong>：A = 29 （或者0b11101）, B = 15（或者0b01111）
<strong> 输出</strong>：2
</pre>

<p> <strong>示例2:</strong></p>

<pre>
<strong> 输入</strong>：A = 1，B = 2
<strong> 输出</strong>：2
</pre>

<p> <strong>提示:</strong></p>

<ol>
<li>A，B范围在[-2147483648, 2147483647]之间</li>
</ol>


## 解法：

异或，然后统计 1 的位数。

```c++
class Solution {
public:
    int convertInteger(int A, int B) {
        unsigned int ab_xor = A ^ B;
        int n_bits = 0;
        while(ab_xor){
            n_bits += 1;
            ab_xor &= ab_xor - 1;
        } 
        return n_bits;
    }
};
```

如果异或完之后只有最高位为 1，如果保存异或结果的是有符号的数，那么 `ab_xor - 1` 就会下溢。因此异或结果需要用无符号数来保存。