---
layout:     post
title:      (leetcode学习第十九天)
subtitle:   (leetcode学习第十九天)
date:       2024-5-10
author:     (pennytask)
header-img: img/wallhaven-werdv6.png
catalog:   true
tags:
    - 学习
---
### [530. 二叉搜索树的最小绝对差](https://leetcode.cn/problems/minimum-absolute-difference-in-bst/)

```cc
class Solution {
public:
    int getMinimumDifference(TreeNode* root) {
       stack<TreeNode*>st;
       int num=INT_MAX;
       TreeNode* pre=nullptr;
       TreeNode* q=root;
       while(q!=nullptr||!st.empty()){
        if(q!=nullptr)
            {st.push(q);
             q=q->left;}
             else{
                q=st.top();
                st.pop();
                if(pre!=nullptr){
                    num=min(num,q->val-pre->val);
                }
                pre=q;
               q=q->right;
             }
       }
      return num;
    }
};
```

   二叉搜索树的最小绝对差必然出现在某节点和它的前序节点，所以中序遍历记录pre节点，更新出栈节点和pre的差值即可

### [501. 二叉搜索树中的众数](https://leetcode.cn/problems/find-mode-in-binary-search-tree/)

```c++
class Solution {
public:
    void searchBST(TreeNode* cur, unordered_map<int, int>& map) { // 前序遍历
    if (cur == NULL) return ;
    map[cur->val]++; // 统计元素频率
    searchBST(cur->left, map);
    searchBST(cur->right, map);
    return ;
}
bool static cmp (const pair<int, int>& a, const pair<int, int>& b) {
    return a.second > b.second; // 按照频率从大到小排序
}

    
    vector<int> findMode(TreeNode* root) {
unordered_map<int, int> map; // key:元素，value:出现频率
        vector<int> result;
        if (root == NULL) return result;
        searchBST(root, map);
        vector<pair<int, int>> vec(map.begin(), map.end());
        sort(vec.begin(), vec.end(), cmp); // 给频率排个序
        result.push_back(vec[0].first);
        for (int i = 1; i < vec.size(); i++) {
            // 取最高的放到result数组中
            if (vec[i].second == vec[0].second) result.push_back(vec[i].first);
            else break;
        }
        return result;
    }
};
```

  直接中序遍历完放在map里，map不能排序，把map复制到vector里，用sort排序，注意sort（头，尾，排序方式）排序方式cmp返回的是一个bool参数，当为1时交换，0时不变，sort使用的是一种快速排序。排序完的头一个就是众数，如果有相同的就都输出。
