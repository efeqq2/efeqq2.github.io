---
layout:     post
title:      (leetcode学习第三十三天)
subtitle:   (leetcode学习第三十三天)
date:       2024-5-20
author:     (pennytask)
header-img: img/wallhaven-1pew8g.jpg
catalog:   true
tags:
    - 学习
---
### [455. 分发饼干](https://leetcode.cn/problems/assign-cookies/)

```c++
class Solution {
public:
    int findContentChildren(vector<int>& g, vector<int>& s) {
        sort(g.begin(), g.end());
        sort(s.begin(), s.end());
         int gnum=0;
         int result=0;
         for(int i=0;i<s.size();i++){
            if(gnum<g.size()){
                if(s[i]>=g[gnum]){gnum++;result++;}
            }
         }
        return result;
    }
};
```

  用小的对应小的

g = [1,2,3], s = [1,1] 中，优先s，在排序完成后，以s中为锚点找能否满足g

### [376. 摆动序列](https://leetcode.cn/problems/wiggle-subsequence/)

```c++
class Solution {
public:
    int wiggleMaxLength(vector<int>& nums) {
        int res = 0;
        int reverse = 0; //初始不知道第一次会上坡还是下坡
        for(int i = 1; i < nums.size(); i++){
            if(nums[i-1]<nums[i] && reverse != 1){
                res++;
                reverse = 1;//记录上坡了
            }
            else if(nums[i-1]>nums[i] && reverse != 2){
                res++;
                reverse = 2;//记录下坡了
            } 
        }
        return res + 1; //res是两两比较得来的值，差一个边界值要+1
    }
};

```

   因为要求的序列严格交替，所以我考虑用bool记录当前是上坡还是下坡，但是用bool一直出错，题解中方法记录的是摆动点的个数，不需要申请额外空间了。

### [53. 最大子数组和](https://leetcode.cn/problems/maximum-subarray/)

```c++
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int res=INT32_MIN;
        int temp=0;
        if(nums.size()==0)return 0;
        if(nums.size()==1)return nums[0];
        for(int i=0;i<nums.size();i++){
                temp=temp+nums[i];
                if(res<temp)res=temp;
                if(temp<0)temp=0;
            }
        
        return res;}
    
};
```

   当记录的temp count<0时，就该把他置为0了，无论如何小于0都是亏得
