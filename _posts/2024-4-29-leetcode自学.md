---
layout:     post
title:      (leetcode学习)
subtitle:   (leetcode学习)
date:       2024-4-20
author:     (pennytask)
header-img: img/the-first.png
catalog:   true
tags:
    - 学习
---

### [239. 滑动窗口最大值](https://leetcode.cn/problems/sliding-window-maximum/)

给你一个整数数组 `nums`，有一个大小为 `k` 的滑动窗口从数组的最左侧移动到数组的最右侧。你只可以看到在滑动窗口内的 `k` 个数字。滑动窗口每次只向右移动一位。

返回 *滑动窗口中的最大值* 。

```
输入：nums = [1,3,-1,-3,5,3,6,7], k = 3
输出：[3,3,5,5,6,7]
解释：
滑动窗口的位置                最大值
---------------               -----
[1  3  -1] -3  5  3  6  7       3
 1 [3  -1  -3] 5  3  6  7       3
 1  3 [-1  -3  5] 3  6  7       5
 1  3  -1 [-3  5  3] 6  7       5
 1  3  -1  -3 [5  3  6] 7       6
 1  3  -1  -3  5 [3  6  7]      7
```

```c++
class Solution {
public:
    vector<int> maxSlidingWindow(vector<int>& nums, int k) {
         vector<int>ans;
         deque<int>q;
         for(int i=0;i<nums.size();i++){
            while(q.empty()!=true&&nums[q.back()]<nums[i]){
                q.pop_back();
            }
            q.push_back(i);
            if(i-q.front()>=k){
                q.pop_front();
            }
            if(i>=k-1){
                ans.push_back(nums[q.front()]);
            }
         }
         return ans;
    }
};
```

- 创建一个双端队列`q`，用于存储当前窗口内的元素索引。
- 遍历数组，对于每个元素，执行以下操作：
  1. 将队列尾部小于等于`nums[i]`的元素索引从队尾弹出，以维护队列的单调性。这样，队列中的元素将按照从大到小的顺序排列，且队首元素将始终是当前窗口中的最大值的索引。
  2. 将当前元素的索引`i`入队。
  3. 如果队首元素离开了当前窗口（即当前索引`i`与队首元素的索引之差大于等于`k`），则将队首元素从队列中弹出，以确保队列中的元素仅包含当前窗口内的元素。
  4. 如果当前索引`i`大于等于`k - 1`，即窗口大小为`k`时，将队首元素对应的数组值`nums[q.front()]`添加到结果数组`ans`中，作为当前窗口的最大值。
- 遍历完成后，返回结果数组`ans`。
- ![Picture1.png](https://pic.leetcode-cn.com/1600878237-pBiBdf-Picture1.png)

