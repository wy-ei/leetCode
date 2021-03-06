---
title: 最长单词
qid: 17.15
tags: [字符串]
---


- 难度：Medium
- 题目链接：[https://leetcode-cn.com/problems/longest-word-lcci/](https://leetcode-cn.com/problems/longest-word-lcci/)


## 题目描述

来源于 [https://leetcode-cn.com/](https://leetcode-cn.com/)

<p>给定一组单词<code>words</code>，编写一个程序，找出其中的最长单词，且该单词由这组单词中的其他单词组合而成。若有多个长度相同的结果，返回其中字典序最小的一项，若没有符合要求的单词则返回空字符串。</p>
<p><strong>示例：</strong></p>
<pre><strong>输入：</strong> ["cat","banana","dog","nana","walk","walker","dogwalker"]
<strong>输出：</strong> "dogwalker"
<strong>解释：</strong> "dogwalker"可由"dog"和"walker"组成。
</pre>
<p><strong>提示：</strong></p>
<ul>
<li><code>0 <= len(words) <= 100</code></li>
<li><code>1 <= len(words[i]) <= 100</code></li>
</ul>


## 解法：

优先搜索长单词，然后使用目前得到的长度来剪枝。最关键的是判断一个长单词能否由一些短单词组成。这里采用了 DFS 和 Trie 来帮助判断。

```c++
class Solution {
public:
    string longestWord(vector<string>& words) {
        Trie<int> trie;
        for(string& w: words){
            trie.put(w);
        }

        sort(words.begin(), words.end(), [](auto& s1, auto& s2){
            return s1.size() > s2.size();
        });

        int max_len = 0;
        string* ret = nullptr;
        for(string& w: words){
            if(max_len > w.size()){
                continue;
            }
            if(max_len == w.size() && (ret == nullptr || w >= *ret)){
                continue;
            }

            if(combine(w, 0, trie)){
                max_len = w.size();
                ret = &w;
            }
        }
        if(ret){
            return *ret;
        }else{
            return string();
        }
    }

    bool combine(string& w, int start, Trie<int>& trie){
        for(int i=start+1;i<w.size();i++){
            if(trie.contains(w.substr(start, i-start))){
                if(combine(w, i, trie)){
                    return true;
                }
            }
        }
        if(start != 0 && trie.contains(w.substr(start, w.size()-start))){
            return true;
        }
        return false;
    }
};
```