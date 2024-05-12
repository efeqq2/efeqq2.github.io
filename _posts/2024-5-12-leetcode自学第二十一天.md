---
layout:     post
title:      (leetcode学习第二十一天)
subtitle:   (leetcode学习第二十一天)
date:       2024-5-12
author:     (pennytask)
header-img: img/wallhaven-wekq8q.jpg
catalog:   true
tags:
    - 学习
---
### [108. 将有序数组转换为二叉搜索树](https://leetcode.cn/problems/convert-sorted-array-to-binary-search-tree/)

给你一个整数数组 `nums` ，其中元素已经按 **升序** 排列，请你将其转换为一棵 

平衡

 二叉搜索树。



 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2021/02/18/btree1.jpg)

```
输入：nums = [-10,-3,0,5,9]
输出：[0,-3,9,-10,null,5]
```

```c++
class Solution {
public:
    TreeNode* traversal(vector<int>& nums,int left,int right){
        if(left>right)return nullptr;
       int mid = left + ((right - left) / 2);
       TreeNode* root = new TreeNode(nums[mid]);
       root->left = traversal(nums, left, mid - 1);
           return root;
    }
    
    TreeNode* sortedArrayToBST(vector<int>& nums) {
            TreeNode *p=traversal(nums,0,nums.size()-1);
            return p;
    }
};
```

  int mid = left + ((right - left) / 2);注意这个

### [538. 把二叉搜索树转换为累加树](https://leetcode.cn/problems/convert-bst-to-greater-tree/)

```c++
class Solution {
public:
    TreeNode* convertBST(TreeNode* root) {
               stack<TreeNode*>st;
               TreeNode* p=root;
                int num=0;
               while(p!=nullptr||!st.empty()){
                if(p!=nullptr){
                    st.push(p);
                    p=p->right;
                }
                else{
                    p=st.top();
                    st.pop();
                    p->val=p->val+num;
                    num=p->val;
                    p=p->left;
                }
               }
               return root;
    }
};
```

### [669. 修剪二叉搜索树](https://leetcode.cn/problems/trim-a-binary-search-tree/)

```c++
class Solution {
public:
    TreeNode* trimBST(TreeNode* root, int low, int high) {
    if (root == NULL) return root; // 确定终止条件
    if (root->val < low) { // 修剪右子树
        return trimBST(root->right, low, high);
    } else if (root->val > high) { // 修剪左子树
        return trimBST(root->left, low, high);
    } else { // 修剪左右子树
        root->left = trimBST(root->left, low, high);
        root->right = trimBST(root->right, low, high);
        return root;
    }
}
};
```

首先，判断根节点是否为空，如果为空，直接返回空。
然后，比较根节点的值和给定范围的最小值和最大值，有三种情况：
如果根节点的值小于最小值，说明根节点和它的左子树都不在范围内，可以直接舍弃。此时，只需要对右子树进行修剪，并返回修剪后的右子树作为新的根节点。
如果根节点的值大于最大值，说明根节点和它的右子树都不在范围内，可以直接舍弃。此时，只需要对左子树进行修剪，并返回修剪后的左子树作为新的根节点。
如果根节点的值在范围内，说明根节点需要保留，但是它的左右子树可能有部分不在范围内，需要进行修剪。此时，递归地对左右子树进行修剪，并将修剪后的左右子树连接到根节点上。
最后，返回修剪后的根节点。

