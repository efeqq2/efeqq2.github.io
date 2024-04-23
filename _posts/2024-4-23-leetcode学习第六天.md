---
layout:     post
title:      (leetcode学习)
subtitle:   (leetcode学习)
date:       2024-4-20
author:     (pennytask)
header-img: img/the-first.png
catalog:   true
tags:
    - 学习
---
### [383. 赎金信](https://leetcode.cn/problems/ransom-note/)

给你两个字符串：`ransomNote` 和 `magazine` ，判断 `ransomNote` 能不能由 `magazine` 里面的字符构成。

如果可以，返回 `true` ；否则返回 `false` 。

`magazine` 中的每个字符只能在 `ransomNote` 中使用一次。

```c++
class Solution {
public:
    bool canConstruct(string ransomNote, string magazine) {
           if(ransomNote.length()>magazine.length())return false; 
            unordered_map<char,int>map1;  // unordered_map<int, int> umap; 
            for(int k=0;k<magazine.length();k++){
                map1[magazine[k]]++;
            }
            for(int p=0;p<ransomNote.length();p++){
                if(map1.find(ransomNote[p])==map1.end()||map1[ransomNote[p]]<=0)
                    return false;
                  else{map1[ransomNote[p]]--;}                  
               
               
            }
                return true;
    }
};
```

哈希表记录magazine的key与value，从ransomNote中寻找。注意map1.find(ransomNote[p])==map1.end()很别扭说是，找了好半天才发现==而不是！=

### [15. 三数之和](https://leetcode.cn/problems/3sum/)

给你一个整数数组 `nums` ，判断是否存在三元组 `[nums[i], nums[j], nums[k]]` 满足 `i != j`、`i != k` 且 `j != k` ，同时还满足 `nums[i] + nums[j] + nums[k] == 0` 。请

你返回所有和为 `0` 且不重复的三元组。

```c++
class Solution {
public:
    int fourSumCount(vector<int>& nums1, vector<int>& nums2, vector<int>& nums3, vector<int>& nums4) {
           int count=0;
           unordered_map<int,int>map1;
           for(int t:nums1){
            for(int k:nums2){
                map1[t+k]++;
            }
           }
           for(int p:nums3){
            for(int q:nums4){
                if(map1.find(0-(p+q))!=map1.end()){
                    count+=map1[0-(p+q)];
                }
            }
           }
           return count;
    }
};
```

哈希表分成两个部分处理。、

### [15. 三数之和](https://leetcode.cn/problems/3sum/)

给你一个整数数组 `nums` ，判断是否存在三元组 `[nums[i], nums[j], nums[k]]` 满足 `i != j`、`i != k` 且 `j != k` ，同时还满足 `nums[i] + nums[j] + nums[k] == 0` 。请

你返回所有和为 `0` 且不重复的三元组。

```c++
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        vector<vector<int>> result;
        sort(nums.begin(), nums.end());
             for (int i = 0; i < nums.size(); i++) {
            if (nums[i] > 0) {
                return result;
            }
            if (i > 0 && nums[i] == nums[i - 1]) {
                continue;
            }
            int left = i + 1;
            int right = nums.size() - 1;
            while (right > left) {
                if (nums[i] + nums[left] + nums[right] > 0) right--;
        else if (nums[i] + nums[left] + nums[right] < 0) left++;
        else {
         result.push_back(vector<int>{nums[i], nums[left], nums[right]});
                    // 去重逻辑应该放在找到一个三元组之后，对b 和 c去重
         while (right > left && nums[right] == nums[right - 1]) right--;
         while (right > left && nums[left] == nums[left + 1]) left++;

                    // 找到答案时，双指针同时收缩
                    right--;
                    left++;
                }
            }

        }
        return result;
    }
};
```

[代码随想录 (programmercarl.com)](https://programmercarl.com/0015.三数之和.html#思路)

忘了就来看，双指针，先排序，再固定一个i。剩下两个指向i后第一个合尾部，主要问题在于去重
