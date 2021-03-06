---
title: 判定是否互为字符重排
qid: 01.02
tags: [数组,字符串]
---


- 难度：Easy
- 题目链接：[https://leetcode-cn.com/problems/check-permutation-lcci/](https://leetcode-cn.com/problems/check-permutation-lcci/)


## 题目描述

来源于 [https://leetcode-cn.com/](https://leetcode-cn.com/)

<p>给定两个字符串 <code>s1</code> 和 <code>s2</code>，请编写一个程序，确定其中一个字符串的字符重新排列后，能否变成另一个字符串。</p>

<p><strong>示例 1：</strong></p>

<pre><strong>输入:</strong> <code>s1</code> = &quot;abc&quot;, <code>s2</code> = &quot;bca&quot;
<strong>输出:</strong> true 
</pre>

<p><strong>示例 2：</strong></p>

<pre><strong>输入:</strong> <code>s1</code> = &quot;abc&quot;, <code>s2</code> = &quot;bad&quot;
<strong>输出:</strong> false
</pre>

<p><strong>说明：</strong></p>

<ul>
	<li><code>0 &lt;= len(s1) &lt;= 100 </code></li>
	<li><code>0 &lt;= len(s2) &lt;= 100 </code></li>
</ul>


## 解法：

```c++
class Solution {
public:
    bool CheckPermutation(string s1, string s2) {
        if(s1.size() != s2.size()){
            return false;
        }
        unordered_map<char,int> mp;
        for(char ch: s1){
            mp[ch] += 1;
        }
        for(char ch: s2){
            mp[ch] -= 1;
            if(mp[ch] == -1){
                return false;
            }
        }
        return true;
    }
};
```