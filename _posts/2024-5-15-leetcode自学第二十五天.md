---
layout:     post
title:      (leetcode学习第二十五天)
subtitle:   (leetcode学习第二十五天)
date:       2024-5-15
author:     (pennytask)
header-img: img/wallhaven-wekq8q.jpg
catalog:   true
tags:
    - 学习
---
### [39. 组合总和](https://leetcode.cn/problems/combination-sum/)

```c++
class Solution {
public:
   vector<int>path;
   vector<vector<int>>res;
    void backtracking(vector<int>& candidates, int target,int sum,int startindex){
       
       if (sum > target) {
    return;
}
       if(sum==target){res.push_back(path);return ;}
       else{
        for(int i=startindex;i<candidates.size();i++){
            sum=sum+candidates[i];
            path.push_back(candidates[i]);
            backtracking(candidates,target,sum,i);
            sum=sum-candidates[i];
            path.pop_back();
        }
       }
    }
    vector<vector<int>> combinationSum(vector<int>& candidates, int target) {
       backtracking(candidates,target,0,0);
       return res;
    }
};
```

  

    if (sum > target) {
    return;

  这是必要的，不然在超过tar时无限循环了。而且这道题目是需要startindex的，不然会给出相同的数量的数字例如[[2,2,3],[2,3,2],[3,2,2],[7]]

  ### [40. 组合总和 II](https://leetcode.cn/problems/combination-sum-ii/)

​       

[   代码随想录 (programmercarl.com)](https://programmercarl.com/0040.组合总和II.html#算法公开课)对应的讲解page

```c++
class Solution {
public:
    vector<vector<int>>res;
    vector<int>path;
    void backtracking(vector<int>& candidates,int target, int sum, int startIndex, vector<bool>& used){
         if(sum==target){res.push_back(path);return;}
         for(int i=startIndex;i < candidates.size()&&sum+candidates[i]<=target ;i++){
            if(i > 0&&candidates[i]==candidates[i-1]&&used[i-1]==false)            continue;
            sum=sum+candidates[i];
            used[i]=true;
             path.push_back(candidates[i]);
            backtracking(candidates,target,sum,i+1,used);
            sum=sum-candidates[i];
            used[i]=false;
            path.pop_back();
         }
    }
    
    
    vector<vector<int>> combinationSum2(vector<int>& candidates, int target) {
       vector<bool> used(candidates.size(), false);
       sort(candidates.begin(),candidates.end());
       backtracking(candidates,target,0,0,used);
       return res;
    }
};
```

   

  明确去重逻辑，是回溯树的横向去重，如果数组已经拍过序，前后两个元素相同，那么前面的回溯已经包括了后面的回溯，所以对横向去重，candidates[i]==candidates[i-1]&&used[i-1]==false这里，当前后两个元素相同，并且used实际上为false时，说明现在是在横向遍历回溯树，竖向遍历时used为true。最后记得在主函数里排下序。

### [131. 分割回文串](https://leetcode.cn/problems/palindrome-partitioning/)

```c++
class Solution {
private:
    vector<vector<string>> result;
    vector<string> path; // 放已经回文的子串
    void backtracking (const string& s, int startIndex) {
        // 如果起始位置已经大于s的大小，说明已经找到了一组分割方案了
        if (startIndex >= s.size()) {
            result.push_back(path);
            return;
        }
        for (int i = startIndex; i < s.size(); i++) {
            if (isPalindrome(s, startIndex, i)) {   // 是回文子串
                // 获取[startIndex,i]在s中的子串
                string str = s.substr(startIndex, i - startIndex + 1);
                path.push_back(str);
            } else {                                // 不是回文，跳过
                continue;
            }
            backtracking(s, i + 1); // 寻找i+1为起始位置的子串
            path.pop_back(); // 回溯过程，弹出本次已经添加的子串
        }
    }
    bool isPalindrome(const string& s, int start, int end) {
        for (int i = start, j = end; i < j; i++, j--) {
            if (s[i] != s[j]) {
                return false;
            }
        }
        return true;
    }
public:
    vector<vector<string>> partition(string s) {
        result.clear();
        path.clear();
        backtracking(s, 0);
        return result;
    }
};
```

  还得二刷这题。都忘了双指针了。还想着要哈希呢

