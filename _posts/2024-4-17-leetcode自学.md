---
layout:     post
title:      (leetcode第一天)
subtitle:   (学习)
date:      2024-4-17
author:     (pennytask)
header-img: img/the-first.png
catalog:   true
tags:
    苦逼学习
---
##### [914. 卡牌分组](https://leetcode.cn/problems/x-of-a-kind-in-a-deck-of-cards/)

给定一副牌，每张牌上都写着一个整数。

此时，你需要选定一个数字 `X`，使我们可以将整副牌按下述规则分成 1 组或更多组：

- 每组都有 `X` 张牌。
- 组内所有的牌上都写着相同的整数。

仅当你可选的 `X >= 2` 时返回 `true`。

```c++
class Solution {
public:
    bool hasGroupsSizeX(vector<int>& deck) {
     int length=deck.size();
     if(length<2)
     {return false;}
      vector<int>count(length+1,0);
    int f=0;
    while(f<length){
         count[deck[f]]++;
         f++;
    }
    int j=0;
    int i=0;
  while(j<length){
    if(count[j]!=0){
        count[i]=count[j];
        i++;j++;
        }
        j++;
  }    
  for (int X = 2; X <= length; ++X) {
            if (length % X == 0) {
                bool flag = 1;
     for(int k=0;k<i;k++){
        if(count[k]%X!=0){
            flag=0;
            break;}
          
     }
       if (flag) {
                    return true;
    }}}
      return false;
  }
      
    };
```

  写的一坨，因为每组都有x张牌，所以正确的解可以被总数整除，同时也可以被每个数字所代表的牌的数量整除。[0,0,0,0,1,1,2,2,3,3]时，最大的公约数即为2。首先通过数组统计每个数字出现的次数，而后排除掉其中的0，最后求整个数组的最小公约数。


