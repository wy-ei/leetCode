---
title: 有重复字符串的排列组合
qid: 08.08
tags: [回溯算法]
---


- 难度：Medium
- 题目链接：[https://leetcode-cn.com/problems/permutation-ii-lcci/](https://leetcode-cn.com/problems/permutation-ii-lcci/)


## 题目描述

来源于 [https://leetcode-cn.com/](https://leetcode-cn.com/)

<p>有重复字符串的排列组合。编写一种方法，计算某字符串的所有排列组合。</p>

<p><strong>示例1:</strong></p>

<pre><strong> 输入</strong>：S = &quot;qqe&quot;
<strong> 输出</strong>：[&quot;eqq&quot;,&quot;qeq&quot;,&quot;qqe&quot;]
</pre>

<p><strong>示例2:</strong></p>

<pre><strong> 输入</strong>：S = &quot;ab&quot;
<strong> 输出</strong>：[&quot;ab&quot;, &quot;ba&quot;]
</pre>

<p><strong>提示:</strong></p>

<ol>
	<li>字符都是英文字母。</li>
	<li>字符串长度在[1, 9]之间。</li>
</ol>


## 解法：

由于字符串中存在重复的字符，上一题 {% include post_link qid="8.07" title="无重复字符串的排列组合" %} 中的方法就需要做些许改进。


### 失败的尝试：基于迭代

基于迭代的方法把新的字符插入到原排列组合的各个位置，以此产生新的排列组合（查考上一题）。但由于存在重复的字符，比如 `aa`，下一个字符如果是 `a`，那么插入位置有 3 个，但是只有一个组合是唯一的。有一种考虑是，向 `aa` 中插入新的字符 `a` 的时候，只在最左端插入。即只在 `perm[i-1] != ch` 的时候才插入。

但是考虑 `SO` 和 `OS`，在第一个后面插入 `S`，第二个前面插入 `S`，得到的都是 `SOS`。因此，上面提到的方法并不可靠。基于迭代的方法尝试失败。


### 可行的解法：回溯法

在选择下一个字符的时候，是从余下的字符集合中选一个，但余下的集合中可能包含重复的字符，选取多个重复的字符作为下一个字符，最终只能得到一种解。因此，只需要在选择下一个字符的时候，把相同的字符只选择一次。相同的其他字符可以作为下下次的选择。

因此，可以在每个 dfs 调用中维护一个集合，记录下当前 dfs 调用中选取过的字符。

```c++
class Solution {
public:
    vector<string> permutation(string s) {
        vector<string> result;
        vector<bool> visited(s.size(), false);
        string path;
        
        dfs(path, s, visited, result);
        return result;
    }

    void dfs(string& path, const string &s, vector<bool>& visited, vector<string>& result){
        if(path.size() == s.size()){
            result.push_back(path);
            return;
        }

        unordered_set<char> vistied_in_this_loop;
        for(int i = 0; i<s.size(); i++){
            if(visited[i]){
                continue;
            }
            if(vistied_in_this_loop.count(s[i]) == 1){
                continue;
            }
            vistied_in_this_loop.insert(s[i]);
            
            visited[i] = true;
            path += s[i];
            dfs(path, s, visited, result);
            visited[i] = false;
            path.pop_back();
        }
    }
};
```

还有一种写法，把字符串排序，然后如果当前字符等于前一个字符，且前一个在上层 dfs 调用中没有被选择过，那就跳过该字符。为啥？因为前一个相同的字符必然在本次 dfs 中被选择过了，后面相同的字符就都不用再选择了。

```c++
class Solution {
public:
    vector<string> permutation(string s) {
        vector<string> result;
        vector<bool> visited(s.size(), false);
        string path;
        
        sort(s.begin(), s.end());
        dfs(path, s, visited, result);
        return result;
    }

    void dfs(string& path, const string &s, vector<bool>& visited, vector<string>& result){
        if(path.size() == s.size()){
            result.push_back(path);
            return;
        }
        
        for(int i = 0;i<s.size();i++){
            if(visited[i]){
                continue;
            }
            if(i > 0 && s[i] == s[i-1] && !visited[i-1]){
                continue;
            }
            visited[i] = true;
            path += s[i];
            dfs(path, s, visited, result);
            visited[i] = false;
            path.pop_back();
        }
    }
};
```