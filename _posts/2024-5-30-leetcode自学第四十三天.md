---
layout:     post
title:      (leetcode学习第四十三天)
subtitle:   (leetcode学习第四十三天)
date:       2024-5-30
author:     (pennytask)
header-img: img/wallhaven-5gpv25.jpg
catalog:   true
tags:
    - 学习
---
### [343. 整数拆分](https://leetcode.cn/problems/integer-break/)

```c++
class Solution {
public:
      long res=1;
      void backtracking(int index,int n,int sum,long temp){    
          if(sum==n){ 
            if(temp>res)res=temp;
              return ;
          }           
          else{
            for(int i=index;i<n&&sum<n;i++){
                sum=sum+i;
                temp=temp*i;
                backtracking(i,n,sum,temp);
                sum=sum-i;
                temp=temp/i;
            }
          }
      }
    
    
    int integerBreak(int n) {
               backtracking(1,n,0,1);
               return res;
    }
};
```

  回溯，暴力，递推公式想不出来。

```c++
class Solution {
public:
    int integerBreak(int n) {
        vector<int> dp(n + 1);
        dp[2] = 1;
        for (int i = 3; i <= n ; i++) {
            for (int j = 1; j <= i / 2; j++) {
                dp[i] = max(dp[i], max((i - j) * j, dp[i - j] * j));
            }
        }
        return dp[n];
    }
};
```

1.dp[i]表示当n=i时，当前乘积最大为dp[i]；

2.递推公式dp[i - j] * j是可能的最大值，所以是从第二个for开始，寻找这个i的最大值，最大值也可能出现在(i - j) * j，同时，因为是遍历寻找最大的dp值，max中应当包含当前遍历的最大dp值来更新，而且在不同的j值和dp[i - j]拆分时，更小的j'值的拆分已经包含了较大的j值的拆分，比如1* 5，1是不可拆分，对于2* 4，4可以拆成1111，而2已经没有必要拆成11了，在1*5中已经包含了。

3.初始化只初始化dp[2] = 1

4.从前向后遍历

### [96. 不同的二叉搜索树](https://leetcode.cn/problems/unique-binary-search-trees/)

 完全看题解属于是[代码随想录 (programmercarl.com)](https://programmercarl.com/0096.不同的二叉搜索树.html#思路)
