---
title: 插入
qid: 05.01
tags: [位运算]
---


- 难度：Easy
- 题目链接：[https://leetcode-cn.com/problems/insert-into-bits-lcci/](https://leetcode-cn.com/problems/insert-into-bits-lcci/)


## 题目描述

来源于 [https://leetcode-cn.com/](https://leetcode-cn.com/)

<p>插入。给定两个32位的整数<code>N</code>与<code>M</code>，以及表示比特位置的<code>i</code>与<code>j</code>。编写一种方法，将<code>M</code>插入<code>N</code>，使得M从N的第j位开始，到第<code>i</code>位结束。假定从<code>j</code>位到<code>i</code>位足以容纳<code>M</code>，也即若M = 10 011，那么j和i之间至少可容纳5个位。例如，不可能出现j = 3和i = 2的情况，因为第3位和第2位之间放不下M。</p>

<p> <strong>示例1:</strong></p>

<pre>
<strong> 输入</strong>：N = 10000000000, M = 10011, i = 2, j = 6
<strong> 输出</strong>：N = 10001001100
</pre>

<p> <strong>示例2:</strong></p>

<pre>
<strong> 输入</strong>： N = 0, M = 11111, i = 0, j = 4
<strong> 输出</strong>：N = 11111
</pre>


## 解法：

把 N 中放置 M 的部分置 0，然后把 M 左移 i 位，与 N 做或操作，就可以得到结果。技术难点在于如何把 N 中对应位置清 0。

假设 `i = 2, j =4`，则窗口大小为 3，可以先得到最低 3 位为 1 的数，然后左移 2 位，再整体取反。具体做法如下：

```
1 << 3 = b1000
b1000 - 1 = b111
b111 << 2 = b11100
~b11100 = b00011
```

想要得到低 i 位为 1 的数，做法为：`(1 << (i+1)) - 1`。如果还是不理解，观察一下 `8` 和 `7` 的二进制表示吧。

下面为实现代码：

```c++
class Solution {
public:
    int insertBits(int N, int M, int i, int j) {
        N = N & ~(((1 << (j-i+1)) - 1) << i);
        N = N | (M << i);
        return N;
    }
};
```

以上代码会在窗口大小为 32 的时候出错，此时即用 M 替换掉 N，因此可以在开头加一行：`if(j-i == 31) return N;`