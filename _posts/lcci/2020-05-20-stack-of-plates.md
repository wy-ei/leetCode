---
title: 堆盘子
qid: 03.03
tags: [设计]
---


- 难度：Medium
- 题目链接：[https://leetcode-cn.com/problems/stack-of-plates-lcci/](https://leetcode-cn.com/problems/stack-of-plates-lcci/)


## 题目描述

来源于 [https://leetcode-cn.com/](https://leetcode-cn.com/)

<p>堆盘子。设想有一堆盘子，堆太高可能会倒下来。因此，在现实生活中，盘子堆到一定高度时，我们就会另外堆一堆盘子。请实现数据结构<code>SetOfStacks</code>，模拟这种行为。<code>SetOfStacks</code>应该由多个栈组成，并且在前一个栈填满时新建一个栈。此外，<code>SetOfStacks.push()</code>和<code>SetOfStacks.pop()</code>应该与普通栈的操作方法相同（也就是说，pop()返回的值，应该跟只有一个栈时的情况一样）。 进阶：实现一个<code>popAt(int index)</code>方法，根据指定的子栈，执行pop操作。</p>

<p>当某个栈为空时，应当删除该栈。当栈中没有元素或不存在该栈时，<code>pop</code>，<code>popAt</code>&nbsp;应返回 -1.</p>

<p><strong>示例1:</strong></p>

<pre><strong> 输入</strong>：
[&quot;StackOfPlates&quot;, &quot;push&quot;, &quot;push&quot;, &quot;popAt&quot;, &quot;pop&quot;, &quot;pop&quot;]
[[1], [1], [2], [1], [], []]
<strong> 输出</strong>：
[null, null, null, 2, 1, -1]
</pre>

<p><strong>示例2:</strong></p>

<pre><strong> 输入</strong>：
[&quot;StackOfPlates&quot;, &quot;push&quot;, &quot;push&quot;, &quot;push&quot;, &quot;popAt&quot;, &quot;popAt&quot;, &quot;popAt&quot;]
[[2], [1], [2], [3], [0], [0], [0]]
<strong> 输出</strong>：
[null, null, null, null, 2, 1, 3]
</pre>


## 解法：

使用一个数组来存放栈即可。

```c++
class StackOfPlates {
public:
    StackOfPlates(int cap):cap_(cap),stacks(0) {}

    void push(int val) {
        if(cap_ == 0) return;
        if(stacks.empty() || stacks.back().size() == cap_){
            stacks.emplace_back(stack<int>());
        }
        stacks.back().push(val);
    }

    int pop() {
        if(stacks.empty()){
            return -1;
        }
        int val = stacks.back().top();
        stacks.back().pop();
        if(stacks.back().empty()){
            stacks.pop_back();
        }
        return val;
    }

    int popAt(int index) {
        if(stacks.size() <= index){
            return -1;
        }
        if(stacks.size() == index + 1 && stacks[index].empty()){
            return -1;
        }
        int val = stacks[index].top();
        stacks[index].pop();
        if(stacks[index].empty()){
            stacks.erase(stacks.begin()+index);
        }
        return val;
    }

private:
    int cap_;
    vector<stack<int>> stacks;
};
```