## 48. 最长不含重复字符的子字符串

- 难度：Medium
- 题目链接：[https://leetcode-cn.com/problems/zui-chang-bu-han-zhong-fu-zi-fu-de-zi-zi-fu-chuan-lcof/](https://leetcode-cn.com/problems/zui-chang-bu-han-zhong-fu-zi-fu-de-zi-zi-fu-chuan-lcof/)


## 题目描述

来源于 [https://leetcode-cn.com/](https://leetcode-cn.com/)

<p>请从字符串中找出一个最长的不包含重复字符的子字符串，计算该最长子字符串的长度。</p>

<p>&nbsp;</p>

<p><strong>示例&nbsp;1:</strong></p>

<pre><strong>输入: </strong>&quot;abcabcbb&quot;
<strong>输出: </strong>3 
<strong>解释:</strong> 因为无重复字符的最长子串是 <code>&quot;abc&quot;，所以其</code>长度为 3。
</pre>

<p><strong>示例 2:</strong></p>

<pre><strong>输入: </strong>&quot;bbbbb&quot;
<strong>输出: </strong>1
<strong>解释: </strong>因为无重复字符的最长子串是 <code>&quot;b&quot;</code>，所以其长度为 1。
</pre>

<p><strong>示例 3:</strong></p>

<pre><strong>输入: </strong>&quot;pwwkew&quot;
<strong>输出: </strong>3
<strong>解释: </strong>因为无重复字符的最长子串是&nbsp;<code>&quot;wke&quot;</code>，所以其长度为 3。
&nbsp;    请注意，你的答案必须是 <strong>子串 </strong>的长度，<code>&quot;pwke&quot;</code>&nbsp;是一个<em>子序列，</em>不是子串。
</pre>

<p>&nbsp;</p>

<p>提示：</p>

<ul>
	<li><code>s.length &lt;= 40000</code></li>
</ul>

<p>注意：本题与主站 3 题相同：<a href="https://leetcode-cn.com/problems/longest-substring-without-repeating-characters/">https://leetcode-cn.com/problems/longest-substring-without-repeating-characters/</a></p>


## 解法：

本题使用滑动窗口即可。

```c++
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        unordered_set<char> window;
        int lo = 0, hi = 0;
        int max_len = 0;
        while(hi < s.size()){
            char ch = s[hi];
            hi++;
            while(window.find(ch) != window.end()){
                window.erase(s[lo]);
                lo ++;
            }
            window.insert(ch);
            max_len = max(max_len, hi - lo);
        }
        return max_len;
    }
};
```

滑动窗口的套路如下：

```c++
int lo = 0, hi = 0;

while(hi < nums.size()){
    char n = nums[hi];
    hi++;
    while(/* 需要收缩窗口 */){
        // 缩小窗口
        // 更新窗口信息
        lo ++;
    }
    window.insert(ch);
    //根据窗口信息，更新答案
}
```