---
title: 字符串压缩
qid: 01.06
tags: [字符串]
---


- 难度：Easy
- 题目链接：[https://leetcode-cn.com/problems/compress-string-lcci/](https://leetcode-cn.com/problems/compress-string-lcci/)


## 题目描述

来源于 [https://leetcode-cn.com/](https://leetcode-cn.com/)

<p>字符串压缩。利用字符重复出现的次数，编写一种方法，实现基本的字符串压缩功能。比如，字符串<code>aabcccccaaa</code>会变为<code>a2b1c5a3</code>。若“压缩”后的字符串没有变短，则返回原先的字符串。你可以假设字符串中只包含大小写英文字母（a至z）。</p>

<p> <strong>示例1:</strong></p>

<pre>
<strong> 输入</strong>："aabcccccaaa"
<strong> 输出</strong>："a2b1c5a3"
</pre>

<p> <strong>示例2:</strong></p>

<pre>
<strong> 输入</strong>："abbccd"
<strong> 输出</strong>："abbccd"
<strong> 解释</strong>："abbccd"压缩后为"a1b2c2d1"，比原字符串长度更长。
</pre>

<p><strong>提示：</strong></p>

<ol>
<li>字符串长度在[0, 50000]范围内。</li>
</ol>


## 解法：

```c++
class Solution {
public:
    string compressString(string s) {
        // 无须压缩
        if(s.size() <= 1){
            return s;
        }

        ostringstream os;
        os << s[0];
        int n = 1;
        for(size_t i=1;i<s.size();i++){
            if(s[i] == s[i-1]){
                n += 1;
            }else{
                os << n << s[i];
                n = 1;
            }
        }
        os << n;
        
        string result = os.str();

        if(result.size() < s.size()){
            return result;
        }else{
            return s;
        }
    }
};
```