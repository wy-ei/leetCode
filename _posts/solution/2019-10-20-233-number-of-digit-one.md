---
title: 数字 1 的个数
qid: 233
tag: [数学]
---

- 难度： 困难
- 通过率： 29.6%
- 题目链接：[https://leetcode-cn.com/problems/number-of-digit-one](https://leetcode-cn.com/problems/number-of-digit-one)


## 题目描述

来源于 [https://leetcode-cn.com/](https://leetcode-cn.com/)

<p>给定一个整数 n，计算所有小于等于 n 的非负整数中数字 1 出现的个数。</p>

<p><strong>示例:</strong></p>

<pre><strong>输入:</strong> 13
<strong>输出:</strong> 6 
<strong>解释: </strong>数字 1 出现在以下数字中: 1, 10, 11, 12, 13 。</pre>



## 解法：

我们考虑数字的每一位上 1 出现的次数。以 2104 这个数字为例：


按位处理，设当前数字为 ABCD，字母分别代表个十百千位。

1\. `D == 4`，此时可设置 `D = 1`，`ABC` 的范围为 `000~210`。

2\. `C == 0`，设置 `C = 1`，`D` 的变化范围为 `0~9`，由于 `C` 从 `0->1`，`AB` 的变化范围要减小，为 `00~20`。共有 `10 * 21 = 210` 种可能。

3\. `B == 1`，此时 `ACD` 的变化范围为 `000~204`。

4\. `A == 2`，设置 `A = 1`，此时 `BCD` 的变化范围是 `000~999`。共有 `1000` 种可能。

设当前处理的位 `i` 上的数为 `n`，设该位前面各位组成的数为 `high`，后面各位构成的数为 `low`。 设 `base` 为 `10^i`，当 n 是个位时 `base=1`。根据以上分析可以总结规律如下：

1. `n == 0`，此时要把该位置为 `1`，`high` 需要减 `1`，`low` 的变化范围是 `0~base-1`。可能的数为 `high * base`。

2. `n == 1`，此时 `high` 在 `0~high-1` 间时，`low` 可以在 `0~base-1` 之间变化。当 `high' == high` 时，`low'` 只能在 `0~low` 之间变化。因此共有 `high * base + low + 1` 中可能。

3. `n > 1`，把该位置为 `1` 后，`high` 可以在 `0~high` 间变化，`low` 可以在 `0~base-1` 间变化，共有 `(high+1) * base` 种可能。

把各个位上为 `1` 的可能数全部加起来，就得到了最终的结果。

基于以上考虑就可以写代码了：

```c++
class Solution {
public:
    int countDigitOne(int num) {
        int low = 0, high = num;
        int n = 0, count = 0, i = 0;
        while(high != 0){
            int base  = pow(10, i);
            n = high % 10;
            low = num - high * base;
            high = high / 10;

            if(n == 0){
                count += high * base;
            }else if(n == 1){
                count += high * base + low + 1;
            }else{
                count += (high+1) * base;
            }
            i++;
        }
        return count;
    }
};
```