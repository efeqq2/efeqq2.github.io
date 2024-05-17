---
layout:     post
title:      (leetcode学习第三十一天)
subtitle:   (leetcode学习第三十一天)
date:       2024-5-17
author:     (pennytask)
header-img: img/wallhaven-m3m8y9.jpg
catalog:   true
tags:
    - 学习
---
### [491. 非递减子序列](https://leetcode.cn/problems/non-decreasing-subsequences/)

```c++
class Solution {
public:
    vector<vector<int>> result;
    vector<int> path;
    void backtracking(vector<int>& nums, int startIndex) {
        if (path.size() > 1) {
            result.push_back(path);}
            // 注意这里不要加return，要取树上的节点
            unordered_set<int>set1;
            for(int i=startIndex;i<nums.size();i++){
                if(!path.empty()&&path.back()>nums[i]||set1.find(nums[i])!=set1.end()){
                    continue;
                }
                set1.insert(nums[i]);
                path.push_back(nums[i]);
                backtracking(nums,i+1);
                path.pop_back();
                
            }
        }
    vector<vector<int>> findSubsequences(vector<int>& nums) {
          backtracking(nums, 0);
        return result;
    }
};
```

​    首先，要求递增子序列至少为2，所以

```cpp
path.size() > 1
```

   其次，使用set来判断当前便利的nums【i】是否在改层已经使用过了，不需要回溯是因为在每层都声明了一次set。

  

### [46. 全排列](https://leetcode.cn/problems/permutations/)

```c++
class Solution {
public:
    vector<int>path;
    vector<vector<int>>res;
   
    void backtracking(vector<int>& nums,vector<bool> used){
       if(path.size()==nums.size())  res.push_back(path);
            for(int i=0;i<nums.size();i++){
                if(used[i]==false){continue;}
                used[i]=false;
                path.push_back(nums[i]);
                backtracking(nums,used);
                used[i]=true;
                path.pop_back();
            }
    }
    
    vector<vector<int>> permute(vector<int>& nums) {
          vector<bool>used(nums.size(),true);
          backtracking(nums,used);
          return res;
    }
};
```

​        不需要index限制起始位置，需要used记录使用过的位置防止重复，而且，res.push那里是可以return的，害我在全排列2那里想了半天为什么又需要return了

### [47. 全排列 II](https://leetcode.cn/problems/permutations-ii/)

```c++
class Solution {
public:
    vector<int>path;
    vector<vector<int>>res;
    void backtracking(vector<int>& nums,vector<bool>& used){
        if(path.size()==nums.size()){res.push_back(path);return ;}
        for(int i=0;i<nums.size();i++){
            if(i>0&&nums[i-1]==nums[i]&&used[i-1]==false)
           { continue;}
            if(used[i]==true){ 
            used[i]=false;
            path.push_back(nums[i]);
            backtracking(nums,used);
            path.pop_back();
            used[i]=true;}
           
        }
    }
    
    vector<vector<int>> permuteUnique(vector<int>& nums) {
            vector<bool>used(nums.size(),true);
            sort(nums.begin(),nums.end());
            backtracking(nums,used);
            return res;
    }
};
```

​      因为有相同的数字还要求不重复，所以又需要排序完使用used。

i>0&&nums[i-1]==nums[i]&&used[i-1]==false

- 这个条件检查了三个条件:

  - `i > 0`: 说明当前处理的是数组中的第二个元素或更靠后的元素。对于第一个元素,这个条件不成立。
  - `nums[i] == nums[i - 1]`: 说明当前元素与前一个元素相同。
  - `used[i - 1] == false`: 说明前一个相同的元素还未被使用过。

- 当这三个条件都满足时,说明我们遇到了同一层中的重复元素。跳过就行

  if(used[i]==true)这是相较于之前的新增的判断，是因为全排列问题，不适用startindex，所以，已经在上一层遍历过的元素，在下一层任然会遍历到，所以需判断是否使用过

