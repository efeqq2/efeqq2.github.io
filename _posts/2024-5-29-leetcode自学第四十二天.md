---
layout:     post
title:      (leetcode学习第四十二天)
subtitle:   (leetcode学习第四十二天)
date:       2024-5-29
author:     (pennytask)
header-img: img/wallhaven-5gpv25.jpg
catalog:   true
tags:
    - 学习
---
### [62. 不同路径](https://leetcode.cn/problems/unique-paths/)

```c++
class Solution {
public:
    int uniquePaths(int m, int n) {
    vector<vector<int>> route(m, vector<int>(n, 0));
    if(m<2||n<2)return 1;
    if(m==2&&n==2)return 2;
    route[0][0]=0;
    for(int i=1;i<m;i++){
      route[i][0]=1;
    }
    for(int j=1;j<n;j++){
      route[0][j]=1;
    }
    for(int i=1;i<m;i++){
        for(int j=1;j<n;j++){
            route[i][j]=route[i-1][j]+route[i][j-1];
        }
    }
          return route[m-1][n-1];
    }
};
```

   1.dp[i][j]应当是当机器人在坐标[i][j]时有dp[i][j]种路径

2. dp[I][J]=dp[i-1][j]+dp[i][j-1];

3. 初始化dp则dp[0][0]为0。对第一列和第一行赋值

4. 从左上到右下遍历。

   ### [63. 不同路径 II](https://leetcode.cn/problems/unique-paths-ii/)

   ```c++
   class Solution {
   public:
       int uniquePathsWithObstacles(vector<vector<int>>& obstacleGrid) {
           int m = obstacleGrid.size();
           int n = obstacleGrid[0].size();
   	if (obstacleGrid[m - 1][n - 1] == 1 || obstacleGrid[0][0] == 1) //如果在起点或终点出现了障碍，直接返回0
               return 0;
           vector<vector<int>> dp(m, vector<int>(n, 0));
           for (int i = 0; i < m && obstacleGrid[i][0] == 0; i++) dp[i][0] = 1;
           for (int j = 0; j < n && obstacleGrid[0][j] == 0; j++) dp[0][j] = 1;
           for (int i = 1; i < m; i++) {
               for (int j = 1; j < n; j++) {
                   if (obstacleGrid[i][j] == 1) continue;
                   dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
               }
           }
           return dp[m - 1][n - 1];
       }
   };
   ```

     与上题类似，当初始化时，第一行或者第一列有障碍物后面的全部都是0，所以将dp数组初始化为全部都是0.遍历时当ob数组中有障碍物直接跳过。
