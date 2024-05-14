---
layout:     post
title:      (leetcode学习第二十三与二十四天)
subtitle:   (leetcode学习第二十三与二十四天)
date:       2024-5-14
author:     (pennytask)
header-img: img/wallhaven-werdv6.png
catalog:   true
tags:
    - 学习
---

### [216. 组合总和 III](https://leetcode.cn/problems/combination-sum-iii/)

```C
class Solution {
public:
   vector<vector<int>> res;
     vector<int> path;
     void backtracking(int n,int k,int startindex ,int sum){
      if(path.size()==k){if(sum==n){res.push_back(path);return;}}
       else{
        for(int i=startindex;i<=9;i++){
            sum=sum+i;
            path.push_back(i);
            backtracking(n,k,i+1,sum);
            path.pop_back();
            sum=sum-i;

        }
      }
     }
   
    vector<vector<int>> combinationSum3(int k, int n) {
       backtracking(n, k, 1, 0);
        return res;
    }
};
```

​       

### [17. 电话号码的字母组合](https://leetcode.cn/problems/letter-combinations-of-a-phone-number/)

```c++
class Solution {
public:
    const string letterMap[10] = {
    "", // 0
    "", // 1
    "abc", // 2
    "def", // 3
    "ghi", // 4
    "jkl", // 5
    "mno", // 6
    "pqrs", // 7
    "tuv", // 8
    "wxyz", // 9
};
     vector<string> result;
     string s;
void backtracking(const string& digits, int index){
    if(s.size()==digits.size()){result.push_back(s);return ;}
    else{
       int num=digits[index]-'0';
       string letter=letterMap[num];
        for(int i=0;i<letter.size();i++){
            s.push_back(letter[i]);
            backtracking(digits,index+1);
            s.pop_back();
        }
    }
}
    vector<string> letterCombinations(string digits) {
    if (digits.size() == 0) {
            return result;
        }
        backtracking(digits, 0);
        return result;
    }
};
```

  与前面组合问题不同的是，这道题实际上是从两个组合中各抽一部分，所以不是使用startindex来去重，而是从头开始，通过index控制选哪个集合。 int num=digits[index]-'0';可以让char变int。
