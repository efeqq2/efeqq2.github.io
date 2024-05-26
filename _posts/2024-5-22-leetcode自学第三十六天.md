---
layout:     post
title:      (leetcode学习第三十六天)
subtitle:   (leetcode学习第三十六天)
date:       2024-5-22
author:     (pennytask)
header-img: img/wallhaven-zyjz7o.jpg
catalog:   true
tags:
    - 学习
---
### [1005. K 次取反后最大化的数组和](https://leetcode.cn/problems/maximize-sum-of-array-after-k-negations/)

```cc
class Solution {
public:
   static bool cmp(int a, int b) {
    return abs(a) > abs(b);
}
    int largestSumAfterKNegations(vector<int>& nums, int k) {
          sort(nums.begin(),nums.end(),cmp);
           int count=0;
           int i=0;
            while(k>0&&i<nums.size()){
                if(nums[i]<0){nums[i]*=-1;k--;}
                i++;
            }
          if(k%2==1){
            nums[nums.size()-1]*=-1;
          }
           
           for(int j=0;j<nums.size();j++){
                count=count+nums[j];
            }
          return count;
    }
};
```

  对nums从大到小的绝对值排序，遍历将负的大的*-1，如果剩余的k还有，就对最后一个动手。
  ### [134. 加油站](https://leetcode.cn/problems/gas-station/)

```c++
class Solution {
public:
    int canCompleteCircuit(vector<int>& gas, vector<int>& cost) {
        for (int i = 0; i < cost.size(); i++) {
            int rest = gas[i] - cost[i]; // 记录剩余油量
            int index = (i + 1) % cost.size();
            while (rest > 0 && index != i) { // 模拟以i为起点行驶一圈（如果有rest==0，那么答案就不唯一了）
                rest += gas[index] - cost[index];
                index = (index + 1) % cost.size();
            }
            // 如果以i为起点跑一圈，剩余油量>=0，返回该起始位置
            if (rest >= 0 && index == i) return i;
        }
        return -1;
    }
};
```

​    **for循环适合模拟从头到尾的遍历，而while循环适合模拟环形遍历，要善于使用while！**

```c++
class Solution {
public:
    int canCompleteCircuit(vector<int>& gas, vector<int>& cost) {
        int curSum = 0;
        int totalSum = 0;
        int start = 0;
        for (int i = 0; i < gas.size(); i++) {
            curSum += gas[i] - cost[i];
            totalSum += gas[i] - cost[i];
            if (curSum < 0) {   // 当前累加rest[i]和 curSum一旦小于0
                start = i + 1;  // 起始位置更新为i+1
                curSum = 0;     // curSum从0开始
            }
        }
        if (totalSum < 0) return -1; // 说明怎么走都不可能跑一圈了
        return start;
    }
};
```

​     如果总油量减去总消耗大于等于零那么一定可以跑完一圈，说明 各个站点的加油站 剩油量rest[i]相加一定是大于等于零的。

每个加油站的剩余量rest[i]为gas[i] - cost[i]。

i从0开始累加rest[i]，和记为curSum，一旦curSum小于零，说明[0, i]区间都不能作为起始位置，因为这个区间选择任何一个位置作为起点，到i这里都会断油，那么起始位置从i+1算起，再从0计算curSum。
### [135. 分发糖果](https://leetcode.cn/problems/candy/)

```c++
class Solution {
public:
    int candy(vector<int>& ratings) {
        vector<int> candyVec(ratings.size(), 1);
        // 从前向后
        for (int i = 1; i < ratings.size(); i++) {
            if (ratings[i] > ratings[i - 1]) candyVec[i] = candyVec[i - 1] + 1;
        }
        // 从后向前
        for (int i = ratings.size() - 2; i >= 0; i--) {
            if (ratings[i] > ratings[i + 1] ) {
                candyVec[i] = max(candyVec[i], candyVec[i + 1] + 1);
            }
        }
        // 统计结果
        int result = 0;
        for (int i = 0; i < candyVec.size(); i++) result += candyVec[i];
        return result;
    }
};
```

需要二刷，实际上不能只通过1次遍历满足需求。相邻两个孩子评分更高的孩子会获得更多的糖果。左右都需要变动，所以需要两次遍历，在结果中取最大值，遍历的边界值需要注意
