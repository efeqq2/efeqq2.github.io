---
layout:     post
title:      (leetcode自学)
subtitle:   (学习)
date:      2024-4-17
author:     (pennytask)
header-img: img/the-first.png
catalog:   true
tags:
    苦逼学习
---
### [209. 长度最小的子数组](https://leetcode.cn/problems/minimum-size-subarray-sum/)

给定一个含有 `n` 个正整数的数组和一个正整数 `target` **。**

找出该数组中满足其总和大于等于 `target` 的长度最小的 **连续****子数组**`[numsl, numsl+1, ..., numsr-1, numsr]` ，并返回其长度**。**如果不存在符合条件的子数组，返回 `0` 。

```c++
class Solution {
public:
    int minSubArrayLen(int target, vector<int>& nums) {
      int length=nums.size();
      int left=0;
      int right=0;
      int count=0;
      int bestnum=INT_MAX;
      while(right<length){
        count=count+nums[right];
        while(count>=target){
           bestnum=min(bestnum,right-left+1);
           count=count-nums[left];
           left++;
        }
        right++;
      }
         if(bestnum==INT_MAX)
          return 0;
          else return bestnum;
    }
};
```

​    滑动窗口，left和right双指针，每当总和超过target，就减去最左端的元素，注意是套用双层循环。

### [59. 螺旋矩阵 II](https://leetcode.cn/problems/spiral-matrix-ii/)

##### 给你一个正整数 `n` ，生成一个包含 `1` 到 `n2` 所有元素，且元素按顺时针顺序螺旋排列的 `n x n` 正方形矩阵 `matrix` 



![img](https://assets.leetcode.com/uploads/2020/11/13/spiraln.jpg)

```c++
class Solution {
public:
    vector<vector<int>> generateMatrix(int n) {
       vector<vector<int>> matrix(n,vector<int>(n));
      int count=1;
      int left=0;
      int right=n-1;
      int up=0;
      int down=n-1;
      while(count<=n*n){
        for(int i=left;i<=right;i++){matrix[up][i]=count;count++;}
        up++;
        for(int i=up;i<=down;i++){matrix[i][right]=count;count++;}
        right--;
        for(int i=right;i>=left;i--){matrix[down][i]=count;count++;}
        down--;
        for(int i=down;i>=up;i--){matrix[i][left]=count;count++;}
        left++;}
        return matrix;
      }
      
    };

```

模拟。边界真的好容易弄错，时不时可以看看。
