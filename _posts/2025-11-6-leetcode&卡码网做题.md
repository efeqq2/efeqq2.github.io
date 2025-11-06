---
layout:     post
title:      (leetcode做题)
subtitle:   (学习)
date:      2025-11-6
author:     (pennytask)
header-img: img/wallhaven-1pew8g.jpg
catalog:   true
tags:
    苦逼学习
---
### 291.小A的序列

#### 题目描述

给一个长度为n的序列和一个整数x，每次操作可以选择序列中的一个元素，将其从序列中删去或者将其值加一。问至少操作多少次，可以使操作后的序列(可以为空)中数字之和是x的倍数。

#### 输入描述

第一行两个用空格隔开的正整数n和x，含义如问题描述中所述。第二行是n个用空格隔开的正整数A[1], A[2], …, A[n]，表示序列中n个元素的值。

1 <= n <= 1000；

1 <= x <= 1000；

1 <= A[i] <= 1000。

#### 输出描述



一行一个整数，表示使序列中数字之和是x的倍数所需要的最少操作数。

```c++
//dfs，时间超限
 int dfs(int i, int j, int n, int x, vector<int>nums, vector<vector<int>>& dp) {
     if (i == n) return j == 0 ? 0 : n;
     if (dp[i][j] >= 0) return dp[i][j];
     int t = j + nums[i];
     return dp[i][j] = min({
         dfs(i + 1, t % x, n, x, nums, dp),
         dfs(i + 1, j, n, x, nums, dp) + 1,
         dfs(i + 1, (t + 1) % x, n, x, nums, dp) + 1
         });
  
 }
```

动态规划+记忆化搜索

  **1.定dp含义**，假设，当前遍历到的数字为t，设dp[i][j] ,i表示遍历到i之前数字的总和，j表示对应这个总和时，取余数为j，dp[i][j]表示当前总和i在余数为j时需要多少次操作。dp[n][0]即为答案。

**2.确定递推公式**，在遍历过程中，对于一个数字，有三种可能，选择，或者删除，或者不变（即直接把他加入到dp[i]和中）

​     ①不变：dp[i][j]=dp[i-1][（j-(t mod x）+x）%x]，不增加操作次数

​     ②选择：dp[i][j] = min(dp[i][j], dp[i - 1][(j - (t % x) - 1 + x) % x] + 1)

​     ③删除：dp[i][j] = min(dp[i][j], dp[i - 1][j] + 1)

```c++
#include<bits/stdc++.h>
#include <vector>
using namespace std;
const int N = 10005, MOD = 1000000007;
using LL = long long;
using PIL = pair<int, LL>;
using PII = pair<int, int>;
int t, ans = 0;
int main() {
    int n, x;
    cin >> n >> x;
    int *nums = new int[n];
    for (int i = 0; i < n; ++i) scanf("%d", nums + i);
    vector<vector<int>> dp(n, vector<int> (x, -1));
    auto dfs = [&](auto&& dfs, int i, int j) -> int {
        if (i == n) return j == 0 ? 0 : n;
        if (dp[i][j] >= 0) return dp[i][j];
        int t = j + nums[i];
        return dp[i][j] = min({dfs(dfs, i + 1, t % x), dfs(dfs, i + 1, j) + 1, dfs(dfs, i + 1, (t + 1) % x) + 1});
    }
    ans = min(n, dfs(dfs, 0, 0));
    cout << ans << endl;
    return 0;
}
```
[120. 三角形最小路径和](https://leetcode.cn/problems/triangle/)

已解答



给定一个三角形 `triangle` ，找出自顶向下的最小路径和。

每一步只能移动到下一行中相邻的结点上。**相邻的结点** 在这里指的是 **下标** 与 **上一层结点下标** 相同或者等于 **上一层结点下标 + 1** 的两个结点。也就是说，如果正位于当前行的下标 `i` ，那么下一步可以移动到下一行的下标 `i` 或 `i + 1` 。

 

**示例 1：**

```
输入：triangle = [[2],[3,4],[6,5,7],[4,1,8,3]]
输出：11
解释：如下面简图所示：
   2
  3 4
 6 5 7
4 1 8 3
自顶向下的最小路径和为 11（即，2 + 3 + 5 + 1 = 11）。
```

**示例 2：**

```
输入：triangle = [[-10]]
输出：-10
```

1.确定dp数组是什么：dp[i][j]表示在当前i，j坐标时，能够取得的最短路径为dp[i][j]。

2.确定动态规划逻辑：dp[I][J]=min（dp[I+1][J],dp[i+][j+1]）+tri[I][J];

3.初始化dp数组：按照tri最后一行的数值初始化，遍历使i，j减小

```c++
class Solution {
public:
   int minimumTotal(vector<vector<int>>& triangle) {
		int rows = triangle.size();
		int cols = triangle[rows - 1].size();
     auto dp = vector<vector<int>>(rows,vector<int>(cols,0));
		for (int i = cols - 1; i >= 0; i--) {
dp[rows - 1][i] = triangle[rows - 1][i];
		}
		
		for (int i = rows - 2; i >= 0;i--) {
for (int j = i; j >= 0; j--) {
	dp[i][j] = min(dp[i + 1][j], dp[i + 1][j + 1]) + triangle[i][j];
}
		}
		return dp[0][0];
 }
};
```
## **314.爱读书**

###### 题目描述

多多很喜欢读书，现在多多有一本书，书有n页，每读完一页，多多都可以获得ai的知识量。正常情况下，多多每分钟可以读完一页，但是多多还有一个能力，可以在一分钟内读完连续两页的内容，只不过能获取的知识量只有正常读完两页知识量之和的二分之一。现在多多只有m分钟的时间用来读完这本书，请你告诉多多他最多可以获得多少的知识。

###### 输入描述

第一行包含两个整数n和m(1 <= n, m <= 1000), 表示书的页数和用来读书的时间。

第二行包含n个数字，每个数字ai(0 <= ai <= 10000)表示第i页的知识量。

###### 输出描述

输出一行，包含一个数字ans，表示最大可获取的知识量，输出的结果保留一位小数，如果在m分钟内不能读完一本书，输出"-1"

###### 输入示例

```
5 3
1 2 3 2 1
```

###### 输出示例

```
6.0
```

用dp解题：

1.确定dp数组代表什么：首先有两个维度,dp[i][j],i代表当前知识量，j代表时间，所以dp[i][j]代表，当前时间为j时获得的最大知识量。

2.确定递推公式：有两种情况，第一种是

```c++
 dp[i][j] = max(dp[i][j], dp[i - 1][j - 1] + nums[i-1]);
```

 另一种是

```c++
dp[i][j] = max(dp[i][j], dp[i - 2][j - 1] + nums[i - 1] / 2.0 + nums[i-2] / 2.0);
```

 3.确定dp[0][0]=0.0，其他所有为-1.0

```c++
int main() {
    cin.tie(nullptr)->sync_with_stdio(false);
    int n, m;
    cin >> n >> m;
    vector<int> nums(n);
    for (int i = 0; i < n; ++i) cin >> nums[i];
    vector<vector<double>>dp(n+1,vector<double>(m+1,-1.0));
	dp[0][0] = 0.0;
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= m; j++) {
            if (dp[i - 1][j - 1] >= 0) {
                dp[i][j] = max(dp[i][j], dp[i - 1][j - 1] + nums[i-1]);

            }

            if (i>=2&&dp[i - 2][j - 1] >= 0) {
				dp[i][j] = max(dp[i][j], dp[i - 2][j - 1] + nums[i - 1] / 2.0 + nums[i-2] / 2.0);
            }

        }
    }

	double ans = -1.0;
    for (int i = 1; i <= m; ++i) ans = max(ans, dp[n][i]);
	if (ans < 0) cout << -1 << endl;
    else {
        printf("%.1lf\n", ans);
    }

    return 0;}
```
### [740. 删除并获得点数](https://leetcode.cn/problems/delete-and-earn/)

给你一个整数数组 `nums` ，你可以对它进行一些操作。

每次操作中，选择任意一个 `nums[i]` ，删除它并获得 `nums[i]` 的点数。之后，你必须删除 **所有** 等于 `nums[i] - 1` 和 `nums[i] + 1` 的元素。

开始你拥有 `0` 个点数。返回你能通过这些操作获得的最大点数。



**示例 1：**

```
输入：nums = [3,4,2]
输出：6
解释：
删除 4 获得 4 个点数，因此 3 也被删除。
之后，删除 2 获得 2 个点数。总共获得 6 个点数。
```

1.确定dp数组代表什么：dp为当前遍历到的最大点数，选择的数字为nums【i】时，能够得到的点数。

2.确定递推公式：要看遍历到的nums【i】跟上一个dp位置选择的元素差值是否为1

​          

```c++
//当选择的元素为上一次选择的元素差值1时
dp[i] = max(dp[i - 1], dp[i - 2] + dp[i] * m[dp[i]]
//或者
dp[i] = dp[i - 1] + dp[i] * m[dp[i]];
```

3.确定初始值ap[0]为第一个元素*他的个数

```c++
 int deleteAndEarn(vector<int>& nums) {
	unordered_map<int, int> m;
	sort(nums.begin(), nums.end());
	vector<int>dp{ 0, nums[0] };
	m[nums[0]] = 1;
	for (int i = 1; i < nums.size(); i++) {
		m[nums[i]]++;
		if (nums[i] != dp.back()) {
			dp.push_back(nums[i]);
		}
	}
	int last = dp[1];
	dp[1] = dp[1] * m[dp[1]];
	for (int i = 2; i < dp.size(); i++) {
		if (dp[i] - last == 1) {
			last = dp[i];
			dp[i] = max(dp[i - 1], dp[i - 2] + dp[i] * m[dp[i]]);
		}
		else {
			last = dp[i];
			dp[i] = dp[i - 1] + dp[i] * m[dp[i]];
		}
	}
	return dp[dp.size() - 1];
}
```






