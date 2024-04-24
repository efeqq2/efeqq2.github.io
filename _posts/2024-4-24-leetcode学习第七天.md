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
### [128. 最长连续序列](https://leetcode.cn/problems/longest-consecutive-sequence/)

给定一个未排序的整数数组 `nums` ，找出数字连续的最长序列（不要求序列元素在原数组中连续）的长度。

请你设计并实现时间复杂度为 `O(n)` 的算法解决此问题。

```c++
class Solution {
public:
    int longestConsecutive(vector<int>& nums) {
        int res = 0;    // 记录最长连续序列的长度
        unordered_set<int> num_set(nums.begin(), nums.end());   // 记录nums中的所有数值
        int seqLen;
        for(int num: num_set){
            // 如果当前的数是一个连续序列的起点，统计这个连续序列的长度
            if(!num_set.count(num - 1)){
                seqLen = 1;     // 连续序列的长度，初始为1
                while(num_set.count(++num))seqLen++;    // 不断查找连续序列，直到num的下一个数不存在于数组中
                res = max(res, seqLen);     // 更新最长连续序列长度
            }
        }
        return res;
    }
};

```

  哈希表，最长连续序列的特点是，如果一个数字的前一个数字在哈希表中，那么他就不是开头，一个数字的下一个数字不在哈希表中，他就是结尾。通过是不是开头决定是否更新res值，一个连续序列最长就哈希表的长度。

```
  unordered_set<int> num_set(nums.begin(), nums.end());
```

  给哈希表赋值的函数

```c++
num_set.count()
```

   与find（）的区别在于，count（）查找一个数字在哈希表中的个数，而map自动去重，所以只会返回1或0，find（）返回指向改元素的指针或者尾指针。
