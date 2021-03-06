---
title: 单词频率
qid: 16.02
tags: [设计,哈希表]
---


- 难度：Medium
- 题目链接：[https://leetcode-cn.com/problems/words-frequency-lcci/](https://leetcode-cn.com/problems/words-frequency-lcci/)


## 题目描述

来源于 [https://leetcode-cn.com/](https://leetcode-cn.com/)

<p>设计一个方法，找出任意指定单词在一本书中的出现频率。</p>

<p>你的实现应该支持如下操作：</p>

<ul>
	<li><code>WordsFrequency(book)</code>构造函数，参数为字符串数组构成的一本书</li>
	<li><code>get(word)</code>查询指定单词在书中出现的频率</li>
</ul>

<p><strong>示例：</strong></p>

<pre>WordsFrequency wordsFrequency = new WordsFrequency({&quot;i&quot;, &quot;have&quot;, &quot;an&quot;, &quot;apple&quot;, &quot;he&quot;, &quot;have&quot;, &quot;a&quot;, &quot;pen&quot;});
wordsFrequency.get(&quot;you&quot;); //返回0，&quot;you&quot;没有出现过
wordsFrequency.get(&quot;have&quot;); //返回2，&quot;have&quot;出现2次
wordsFrequency.get(&quot;an&quot;); //返回1
wordsFrequency.get(&quot;apple&quot;); //返回1
wordsFrequency.get(&quot;pen&quot;); //返回1
</pre>

<p><strong>提示：</strong></p>

<ul>
	<li><code>book[i]</code>中只包含小写字母</li>
	<li><code>1 &lt;= book.length &lt;= 100000</code></li>
	<li><code>1 &lt;= book[i].length &lt;= 10</code></li>
	<li><code>get</code>函数的调用次数不会超过100000</li>
</ul>


## 解法：

可以使用一个 map 统计词频，也可以使用一个 trie 来存储所有的单词，并统计词频。


```c++

struct Node{
    Node():count(0){}
    int count;
    Node* children[26]{};
};

class Trie{
private:
public:
    void insert(const string& word){
        Node *node = &root;
        for(auto ch: word){
            int i = ch - 'a';
            if(node->children[i] == nullptr){
                node->children[i] = new Node;
            }
            node = node->children[i];
        }
        node->count += 1;
    }

    int find(const string& word){
        Node *node = &root;
        for(auto ch: word){
            int i = ch - 'a';
            if(node->children[i]){
                node = node->children[i];
            }else{
                return 0;
            }
        }
        return node->count;
    }
private:
    Node root;
};


class WordsFrequency {
public:
    WordsFrequency(vector<string>& book) {
        for(auto& word: book){
            trie.insert(word);
        }
    }
    int get(string word) {
        return trie.find(word);
    }
private:
    Trie trie;
};
```