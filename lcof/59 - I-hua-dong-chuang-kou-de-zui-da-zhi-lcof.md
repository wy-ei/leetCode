## 59 - I. 滑动窗口的最大值

- 难度：Easy
- 题目链接：[https://leetcode-cn.com/problems/hua-dong-chuang-kou-de-zui-da-zhi-lcof/](https://leetcode-cn.com/problems/hua-dong-chuang-kou-de-zui-da-zhi-lcof/)


## 题目描述

来源于 [https://leetcode-cn.com/](https://leetcode-cn.com/)

<p>给定一个数组 <code>nums</code> 和滑动窗口的大小 <code>k</code>，请找出所有滑动窗口里的最大值。</p>

<p><strong>示例:</strong></p>

<pre><strong>输入:</strong> <em>nums</em> = <code>[1,3,-1,-3,5,3,6,7]</code>, 和 <em>k</em> = 3
<strong>输出: </strong><code>[3,3,5,5,6,7] 
<strong>解释: 
</strong></code>
  滑动窗口的位置                最大值
---------------               -----
[1  3  -1] -3  5  3  6  7       3
 1 [3  -1  -3] 5  3  6  7       3
 1  3 [-1  -3  5] 3  6  7       5
 1  3  -1 [-3  5  3] 6  7       5
 1  3  -1  -3 [5  3  6] 7       6
 1  3  -1  -3  5 [3  6  7]      7</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<p>你可以假设 <em>k </em>总是有效的，在输入数组不为空的情况下，1 &le; k &le;&nbsp;输入数组的大小。</p>

<p>注意：本题与主站 239 题相同：<a href="https://leetcode-cn.com/problems/sliding-window-maximum/">https://leetcode-cn.com/problems/sliding-window-maximum/</a></p>


## 解法一：暴力求解

在每个窗口中寻找最大值。

```c++
class Solution {
public:
    vector<int> maxSlidingWindow(vector<int>& nums, int k) {
        vector<int> ret;
        if(k == 0 || nums.size() == 0) return ret;

        for(auto it = nums.begin(); it + k != nums.end()+1; ++it){
            int max_val = *max_element(it, it + k);
            ret.push_back(max_val);
        }

        return ret;
    }
};
```

## 解法二：单调队列

“单调队列”这个名词是我在 leetcode 上看到的，意思是队列中中数，是单调递增(减)的。

本题中，维护一个单调递减的队列。如果 `n` 小于队列尾部的元素，那就把 `n` 入队，否则一直出队，直到 `n` 小于队尾元素或者队列为空，然后把 `n` 入队列。可以想象，队头就是最大的元素。如果滑动窗口中滑出窗口的值等于队列头部，那就移除队列头部的值。此时队列中余下的值，一定在删除掉的这个值的右边，因此一定在滑动窗口内部。

```c++
class Solution {
public:
    vector<int> maxSlidingWindow(vector<int>& nums, int k) {
        vector<int> ret;
        ret.reserve(nums.size() - k);
        if(k == 0 || nums.size() == 0) return ret;
        deque<int> deq;

        for(int i = 0;i < nums.size(); i++){
            int n = nums[i];

            while (!deq.empty() && deq.back() < n){
                deq.pop_back();
            }

            deq.push_back(n);

            if(i >= k &&  deq.front() == nums[i-k]){
                deq.pop_front();
            }


            if(i >= k - 1){
                ret.push_back(deq.front());
            }
        }

        return ret;
    }
};
```