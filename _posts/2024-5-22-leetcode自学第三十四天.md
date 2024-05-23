---
layout:     post
title:      (leetcode学习第三十四天)
subtitle:   (leetcode学习第三十四天)
date:       2024-5-21
author:     (pennytask)
header-img: img/wallhaven-m3m8y9.jpg
catalog:   true
tags:
    - 学习
---
### [122. 买卖股票的最佳时机 II](https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-ii/)

```c++
class Solution {
public:
    int maxProfit(vector<int>& prices) {
         int res=0;
         if(prices.size()<=1)return 0;
         for(int i=1;i<prices.size();i++){
            if(prices[i]-prices[i-1]>0){
                res=res+prices[i]-prices[i-1];
            }
         }
         return res;
    }
};
```

  想不到，真的想不到。

**把利润分解为每天为单位的维度，而不是从 0 天到第 3 天整体去考虑！**

 第 0 天买入，第 3 天卖出，那么利润为：prices[3] - prices[0]。

相当于(prices[3] - prices[2]) + (prices[2] - prices[1]) + (prices[1] - prices[0])。![122.买卖股票的最佳时机II](https://code-thinking-1253855093.file.myqcloud.com/pics/2020112917480858-20230310134659477.png)

### [55. 跳跃游戏](https://leetcode.cn/problems/jump-game/)

```c++
class Solution {
public:
    bool canJump(vector<int>& nums) {
        int cover = 0;
        if (nums.size() == 1) return true; // 只有一个元素，就是能达到
        for (int i = 0; i <= cover; i++) { // 注意这里是小于等于cover
            cover = max(i + nums[i], cover);
            if (cover >= nums.size() - 1) return true; // 说明可以覆盖到终点了
        }
        return false;
    }
};
```

想的是明白的，写没写明白，每次都要走最远的，但是如何更新写的不明白，应当是在能够遍历到的范围内，对每个能覆盖到的元素所能覆盖的范围进行比较。
### [45. 跳跃游戏 II](https://leetcode.cn/problems/jump-game-ii/)

```c++
class Solution {
public:
    int jump(vector<int>& nums) {
         if (nums.size() == 1) return 0;
        int curDistance = 0;    // 当前覆盖最远距离下标
        int ans = 0;            // 记录走的最大步数
        int nextDistance = 0;
        for(int i=0;i<nums.size();i++){
            nextDistance=max(nums[i]+i,nextDistance);
            if(i==curDistance){
                curDistance=nextDistance;
                ans++;
                if (nextDistance >= nums.size() - 1) break;
            }
            
        }
        return  ans;
    }
};
```

   在每一步对比当前遍历到的最远距离，如果当前遍历的数据已经是上一步所能遍历的最远位置，那么就要考虑更新下一次遍历的区间，并且判断是否要结束，当下一步所能遍历的最大范围已经到终点，跳出即可。


