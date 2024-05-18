---
layout:     post
title:      (leetcode学习第三十二天)
subtitle:   (leetcode学习第三十二天)
date:       2024-5-18
author:     (pennytask)
header-img: img/wallhaven-zyjz7o.jpg
catalog:   true
tags:
    - 学习
---
### [332. 重新安排行程](https://leetcode.cn/problems/reconstruct-itinerary/)

给你一份航线列表 `tickets` ，其中 `tickets[i] = [fromi, toi]` 表示飞机出发和降落的机场地点。请你对该行程进行重新规划排序。

所有这些机票都属于一个从 `JFK`（肯尼迪国际机场）出发的先生，所以该行程必须从 `JFK` 开始。如果存在多种有效的行程，请你按字典排序返回最小的行程组合。

- 例如，行程 `["JFK", "LGA"]` 与 `["JFK", "LGB"]` 相比就更小，排序更靠前。

假定所有机票至少存在一种合理的行程。且所有的机票 必须都用一次 且 只能用一次。

 

```c++
class Solution {
public:
      unordered_map<string,map<string,int>> targets;
       bool backtracking(int ticketNum, vector<string>& result){
        if(result.size()==ticketNum+1)return true;
        for(pair<const string,int>&target:targets[result[result.size()-1]]){
            if(target.second>0){
                result.push_back(target.first);
                target.second--;
               if(backtracking(ticketNum,result))return true ;
                target.second++;
                result.pop_back();
            }
        }
        return false;
      }
    
    vector<string> findItinerary(vector<vector<string>>& tickets) {
            vector<string> result;
        for (const vector<string>& vec : tickets) {
            targets[vec[0]][vec[1]]++; // 记录映射关系
        }
         result.push_back("JFK"); // 起始机场
        backtracking(tickets.size(), result);
        return result;
    }
};
```

​      主要思路看[代码随想录 (programmercarl.com)](https://programmercarl.com/0332.重新安排行程.html#思路)

  

```c++
假设现在 result 向量中的行程是 ["JFK", "SFO"]。根据给定的 targets 字典:

unordered_map<string, unordered_map<string, int>> targets = {
    {"JFK", {{"SFO", 2}, {"ATL", 3}}},
    {"SFO", {{"ATL", 2}}},
    {"ATL", {{"JFK", 1}, {"SFO", 1}}}
};
```

1. 第一次循环,`target` 会被赋值为 `{"ATL", 2}`。由于 `target.second > 0` 为 true,说明我们还可以从 `"SFO"` 飞往 `"ATL"` 这个目的地。
2. 接下来,我们将 `"ATL"` 添加到 `result` 向量的末尾,得到 `["JFK", "SFO", "ATL"]`。同时,将 `target.second` 减 1,变为 1。
3. 然后,递归调用 `backtracking` 函数,继续尝试扩展这个行程。

​       这个 for 循环只有一次遍历,因为 `targets[result[result.size() - 1]]` 只包含了一个 `"ATL"` 目的地。





```
for (const vector<string>& vec : tickets) {
            targets[vec[0]][vec[1]]++; // 记录映射关系
        }
```

   语法问题，map的查询只通过key值进行

```c++
vector<vector<string>> tickets = {
    {"JFK", "SFO"},
    {"JFK", "ATL"},
    {"SFO", "ATL"},
    {"ATL", "JFK"},
    {"ATL", "SFO"}
};

```

​    迭代器vec每次给出一对，所以targets[vec[0]][vec[1]][vec[1]]，而且map在访问时，先查询vec[0]是否存在，不存在就创建一个，然后继续查找vec[1]没有就创建一个，++时是对value++，所以直接加到int上



​    迭代器vec每次给出一对，所以targets[vec[0]][vec[1]][vec[1]]，而且map在访问时，先查询vec[0]是否存在，不存在就创建一个，然后继续查找vec[1]没有就创建一个，++时是对value++，所以直接加到int上
