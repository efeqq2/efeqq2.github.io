---
layout:     post
title:      (leetcode学习第二十六天)
subtitle:   (leetcode学习第二十六天)
date:       2024-5-16
author:     (pennytask)
header-img: img/
catalog:   true
tags:
    - 学习
---
### [93. 复原 IP 地址](https://leetcode.cn/problems/restore-ip-addresses/)

```c++
class Solution {
public:
     vector<string> result;
    void backtracking(string& s, int startIndex, int pointNum){
     if (pointNum == 3) { // 逗点数量为3时，分隔结束
            // 判断第四段子字符串是否合法，如果合法就放进result中
            if (isValid(s, startIndex, s.size() - 1)) {
                result.push_back(s);
            }
            return;
        }
        else{
            for(int i=startIndex;i<s.size();i++){
                if(isValid(s,startIndex,i)){
                    s.insert(s.begin() + i + 1 , '.');
                    pointNum++;
                    backtracking(s,i+2,pointNum);
                     pointNum--;                         // 回溯
                    s.erase(s.begin() + i + 1);
                }
                else break;
            }
        }
    }
    bool isValid(const string& s, int start, int end) {
        if (start > end) {
            return false;
        }
        if (s[start] == '0' && start != end) { // 0开头的数字不合法
                return false;
        }
        int num = 0;
        for (int i = start; i <= end; i++) {
            if (s[i] > '9' || s[i] < '0') { // 遇到非数字字符不合法
                return false;
            }
            num = num * 10 + (s[i] - '0');
            if (num > 255) { // 如果大于255了不合法
                return false;
            }
        }
        return true;}

    vector<string> restoreIpAddresses(string s) {
        result.clear();
        if (s.size() < 4 || s.size() > 12) return result; // 算是剪枝了
        backtracking(s, 0, 0);
        return result;
    }
};
```

一学就会一写就废，还得二刷

### [78. 子集](https://leetcode.cn/problems/subsets/)

```c++
class Solution {
public:
    vector<int>path;
    vector<vector<int>>res;
    void backtracking(vector<int>nums,int startindex){
       res.push_back(path);
        for(int i=startindex;i<nums.size();i++){
            path.push_back(nums[i]);
            backtracking(nums,i+1);
            path.pop_back();
        }
    }
    vector<vector<int>> subsets(vector<int>& nums) {
           backtracking(nums,0);
           return res;
    }
};
```

### [90. 子集 II](https://leetcode.cn/problems/subsets-ii/)

```c++
class Solution {
public:
    vector<int>path;
    vector<vector<int>>res;
  void backtracking(vector<int>& nums,int startindex,vector<bool>used){
      res.push_back(path);
      for(int i=startindex;i<nums.size();i++){
        if(i>0&&nums[i]==nums[i-1]&&used[i-1]==false){
           continue;
        }
           path.push_back(nums[i]);
           used[i]=true;
             backtracking(nums,i+1,used);
             used[i]=false;
             path.pop_back();
      }
    }
    vector<vector<int>> subsetsWithDup(vector<int>& nums) {
       vector<bool> used(nums.size(), false);
        sort(nums.begin(), nums.end()); // 去重需要排序
        backtracking(nums, 0, used);
        return res;
    }
};
```

  与前面相同，当需要满足没有重复的子集时，就应该排序然后使用used
