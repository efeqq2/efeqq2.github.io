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
### [242. 有效的字母异位词](https://leetcode.cn/problems/valid-anagram/)

##### 给定两个字符串 `*s*` 和 `*t*` ，编写一个函数来判断 `*t*` 是否是 `*s*` 的字母异位词。

```c++
public:
    bool isAnagram(string s, string t) {
          if(s.length()!=t.length()) return false;
          unordered_map<char,int>dic;
          for(char c:s){
            dic[c]=dic[c]+1;
            }
            for (char c:t) {
            dic[c] -= 1;
        }
         for (auto kv : dic) {
            if (kv.second != 0)
                return false;
        }
       return true;
    }
```

使用哈希表，每次遍历到一个字母就在表中对应位+1，遍历另一个字符串时在对应位置-1，若是相同，最后表中只有0

### [349. 两个数组的交集](https://leetcode.cn/problems/intersection-of-two-arrays/)

##### 给定两个数组 `nums1` 和 `nums2` ，返回 *它们的* *交集*

```c++
   vector<int> intersection(vector<int>& nums1, vector<int>& nums2) {
        unordered_set<int> result_set; 
        int hash[1005] = {0}; // 默认数值为0
        for(int c:nums1){
            hash[c]=1;
        }
         for (int num : nums2) { // nums2中出现话，result记录
            if (hash[num] == 1) {
                result_set.insert(num);
            }
         }
           return vector<int>(result_set.begin(), result_set.end());
    }
```

  哈希表，学到了增强型for循环， 注意for (int num : nums2）中，num相当于一个指针指向nums[i]

hash[num] == 1相当于普通循环中hash[nums[i]]==1.

   所以，增强型for循环不需要下标也不能使用下标，需要下标就不要使用它。当使用哈希表进行遍历时不需要下标， unordered_set<int> result_set底层实现是一个哈希表，[C++ vector的用法（整理）-CSDN博客](https://blog.csdn.net/wkq0825/article/details/82255984)。

### [202. 快乐数](https://leetcode.cn/problems/happy-number/)

编写一个算法来判断一个数 `n` 是不是快乐数。

**「快乐数」** 定义为：

- 对于一个正整数，每一次将该数替换为它每个位置上的数字的平方和。

- 然后重复这个过程直到这个数变为 1，也可能是 **无限循环** 但始终变不到 1。

- 如果这个过程 **结果为** 1，那么这个数就是快乐数。

  ```c++
  class Solution {
  public:
  
       int step(int n){
         int sum=0;
          while(n>0){
              int temp=n%10;
              sum=sum+temp*temp;
              n=n/10;
          }
          return sum;
       }
      bool isHappy(int n) {
  
          int num1=n;   
          if(n==1)return true;
          int num2=step(num1);   
          while(num1!=num2){
             if(num1==1||num2==1){return true;}
           else{ num1=step(num1);
                 num2=step(num2);
                 num2=step(num2); 
             } 
          }
          return false;
      }
  };
  ```

    快慢指针，因为数字只有1到9，每位平方下来是有限的数字，最后会循环，所以与判断环的方法相似，一个走两步一个走一步，直到相遇，途中不存在为一是false。

  ### 方法2

  ```c++
   bool isHappy(int n) {
        unordered_set<int> set;
          while(1) {
              int sum = step(n);
              if (sum == 1) {
                  return true;
              }
              // 如果这个sum曾经出现过，说明已经陷入了无限循环了，立刻return false
              if (set.find(sum) != set.end()) {
                  return false;
              } else {
                  set.insert(sum);
              }
              n = sum;
      }}
  ```

   将每一次的计算结果储存在哈希表中，如果重复，返回false，（find（）函数如果找到了返回改数的位置，没找到返回哈希表的尾部指针）
