---
layout:     post
title:      (文章标题)
subtitle:   (副标题)
date:       2018-12-01
author:     (作者名)
header-img: img/the-first.png
catalog:   true
tags:
    - 往事如烟
---

## 数组理论基础，[704. 二分查找](https://leetcode.cn/problems/binary-search/)[35. 搜索插入位置](https://leetcode.cn/problems/search-insert-position/)[977. 有序数组的平方](https://leetcode.cn/problems/squares-of-a-sorted-array/)

##### 704 给定一个 `n` 个元素有序的（升序）整型数组 `nums` 和一个目标值 `target` ，写一个函数搜索 `nums` 中的 `target`，如果目标值存在返回下标，否则返回 `-1`。

```c++
class Solution {
public:
    int search(vector<int>& nums, int target) {
   int left=0;
   int right=nums.size()-1;
   while(left<=right){
    int mid=(left+right)/2;
    if(nums[mid]>target){right=mid-1;}
    else if(nums[mid]<target){left=mid+1;}
    else return mid;
   }
   return -1;
    }
};
```

  主要问题在于边界的划分，有两种划分方法，第一种是左闭右闭区间**[left, right]**，这种情况下left<=right,且right为size-1（因为闭区间时左右相等有效）。第二种是左闭右开区间[left, right) ，此时left<right.

##### 35  给定一个排序数组和一个目标值，在数组中找到目标值，并返回其索引。如果目标值不存在于数组中，返回它将会被按顺序插入的位置。请必须使用时间复杂度为 `O(log n)` 的算法。

```c++
class Solution {
public:
    int searchInsert(vector<int>& nums, int target) {
     int left=0;
     int right=nums.size()-1;
     while(left<=right){
        int mid=(left+right)/2;
        if(nums[mid]<target)
          left=mid+1;
          else if(nums[mid]>target)
          right=mid-1;
          else return mid;
     }
      return right + 1;
    }
};
```

##### 977 给你一个按 **非递减顺序** 排序的整数数组 `nums`，返回 **每个数字的平方** 组成的新数组，要求也按 **非递减顺序** 排序。

```c++
class Solution {
public:
    vector<int> sortedSquares(vector<int>& nums) {
        int n = nums.size() - 1;
        vector<int> result(n + 1, 0);
        int left = 0, right = n;
        while(left <= right) {
            int a = nums[left] * nums[left];
            int b = nums[right] * nums[right];
            if(a >= b){
                result[n--] = a;
                left++;
            }
            else{
                result[n--] = b;
                right--;
            }
        }
        return result;
    }
};
```

  两边数字的平方一定是其中最大的，所以双指针。
