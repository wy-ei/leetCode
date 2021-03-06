---
title: 最短超串
qid: 17.18
---


- 难度：Medium
- 题目链接：[https://leetcode-cn.com/problems/shortest-supersequence-lcci/](https://leetcode-cn.com/problems/shortest-supersequence-lcci/)


## 题目描述

来源于 [https://leetcode-cn.com/](https://leetcode-cn.com/)

<p>假设你有两个数组，一个长一个短，短的元素均不相同。找到长数组中包含短数组所有的元素的最短子数组，其出现顺序无关紧要。</p>

<p>返回最短子数组的左端点和右端点，如有多个满足条件的子数组，返回左端点最小的一个。若不存在，返回空数组。</p>

<p><strong>示例 1:</strong></p>

<pre><strong>输入:</strong>
big = <code>[7,5,9,0,2,1,3,<strong>5,7,9,1</strong>,1,5,8,8,9,7]
small = [1,5,9]</code>
<strong>输出: </strong>[7,10]</pre>

<p><strong>示例 2:</strong></p>

<pre><strong>输入:</strong>
big = <code>[1,2,3]
small = [4]</code>
<strong>输出: </strong>[]</pre>

<p><strong>提示：</strong></p>

<ul>
	<li><code>big.length&nbsp;&lt;= 100000</code></li>
	<li><code>1 &lt;= small.length&nbsp;&lt;= 100000</code></li>
</ul>


## 解法：

滑动窗口，以下几种情况需要移动左边界：

1. `big[lo]` 不在 `small` 中
2. `big[lo]` 在 lo~hi 之间出现了多次

```c++
class Solution {
public:
    vector<int> shortestSeq(vector<int>& big, vector<int>& small) {
        unordered_set<int> small_set(small.begin(), small.end());
        unordered_map<int, int> window;
        cout << big.size();
        int lo = 0;
        int min_len = big.size()+1;
        int min_lo = 0;

        for(int hi=0;hi<big.size();hi++){
            if(small_set.count(big[hi])){
                window[big[hi]]++;
            }
            while(lo < hi) {
                int n = big[lo];
                if (small_set.count(n) == 0) {
                    lo++;
                } else if (window.find(n) != window.end() && window[n] > 1) {
                    lo++;
                    window[n]--;
                }else{
                    break;
                }
            }
            if(window.size() == small.size()  &&  (hi - lo + 1) < min_len){
                min_len = hi - lo + 1;
                min_lo = lo;
            }
        }

        if(min_len == big.size()+1){
            return {};
        }else{
            return {min_lo, min_lo + min_len - 1};
        }
    }
};
```