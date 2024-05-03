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
### 二叉树递归遍历

##### 前序

```c++
class Solution {
public:
     void Traversal(TreeNode* cur,vector<int>&res){
        if(cur==nullptr)return ;
        else  res.push_back(cur->val);
         Traversal(cur->left,res);
         Traversal(cur->right,res);
     }
   
    vector<int> preorderTraversal(TreeNode* root) {
           vector<int>res1;
           Traversal(root,res1);
           return res1;
     
    }
};
```

##### 中序

```c++
  void Traversal(TreeNode* cur,vector<int>&res){
        
        if(cur==nullptr)return ;
         Traversal(cur->left,res);
         res.push_back(cur->val);       
         Traversal(cur->right,res);
     }
```

##### 后序

```c++
  void Traversal(TreeNode* cur,vector<int>&res){
        
        if(cur==nullptr)return ;
         Traversal(cur->left,res);        
         Traversal(cur->right,res);
          res.push_back(cur->val);      
     }
```

### 迭代

#####   前序

```c++
class Solution {
public:
     vector<int> preorderTraversal(TreeNode* root) {
        stack<TreeNode*> st;
        vector<int> result;
        if (root == NULL) return result;
        st.push(root);
        while (!st.empty()) {
            TreeNode* node = st.top();                       
            st.pop();
            result.push_back(node->val);
            if (node->right) st.push(node->right);          
            if (node->left) st.push(node->left);            
        }
        return result;
    }
};
```
##### 中序迭代

```c++
class Solution {
public:
    vector<int> inorderTraversal(TreeNode* root) {
           vector<int>res;
         stack<TreeNode*>st;
         if(root==nullptr){
           return res;
         }
      
         TreeNode *cur=root;
         while(!st.empty()||cur!=nullptr){
           if(cur!=nullptr){
            st.push(cur);
            cur=cur->left;
           }
           else{
             cur=st.top();
             st.pop();
             res.push_back(cur->val);
             cur=cur->right;
           }
         }
         return res;
    
    }
};
```



