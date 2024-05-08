---
layout:     post
title:      (leetcode学习第十八天)
subtitle:   (leetcode学习第十八天)
date:       2024-5-8
author:     (pennytask)
header-img: wallhaven-l8v3ey.png
catalog:   true
tags:
    - 学习
---
### [617. 合并二叉树](https://leetcode.cn/problems/merge-two-binary-trees/)

##### 迭代

```c++
class Solution {
public:
    TreeNode* mergeTrees(TreeNode* root1, TreeNode* root2) {
                queue<TreeNode*>que;          
                if (root1 == NULL) return root2;
                if (root2 == NULL) return root1;
                que.push(root1);
                que.push(root2);
                while(!que.empty()){
                 TreeNode *p=que.front();
                 que.pop();
                 TreeNode *q=que.front();
                 que.pop();
                 p->val=p->val+q->val;    
                 if(p->left!=nullptr&&q->left!=nullptr){
                    que.push(p->left);
                    que.push(q->left);
                 }
                 if(p->right!=nullptr&&q->right!=nullptr){
                    que.push(p->right);
                    que.push(q->right);
                 }
                 if(p->left==nullptr&&q->left!=nullptr){
                    p->left=q->left;
                 }
                 if(p->right==nullptr&&q->right!=nullptr){
                    p->right=q->right;
                 }
                }
                return root1;

    }
};
```

  迭代在root1上进行更改，就不需要讨论root1不为空，root2为空的情况了。

##### 递归

```c++
class Solution {
public:
    TreeNode* mergeTrees(TreeNode* root1, TreeNode* root2) {
            if(root1==nullptr)return root2;
            if(root2==nullptr)return root1;
            TreeNode* root = new TreeNode(0);
          root->val=root1->val+root2->val;
          root->left=mergeTrees(root1->left,root2->left);
          root->right=mergeTrees(root1->right,root2->right);
         return root;
    }
};
```

### [654. 最大二叉树](https://leetcode.cn/problems/maximum-binary-tree/)

```c++
class Solution {
public:
   
   TreeNode* traversal(vector<int>& nums, int left, int right) {
    if (left >= right) return nullptr;
    int maxsizeindex=left;
    for(int i=left+1;i<right;i++){
        if(nums[i]>nums[maxsizeindex])
        maxsizeindex=i;  
   }
       TreeNode* root = new TreeNode(nums[maxsizeindex]);
       root->left=traversal(nums,left,maxsizeindex);
       root->right=traversal(nums,maxsizeindex+1,right);
       return root;
   }
    TreeNode* constructMaximumBinaryTree(vector<int>& nums) {
       return traversal(nums, 0, nums.size());
    }
};
```

最大的问题还是区间，要坚持左闭右开

### [700. 二叉搜索树中的搜索](https://leetcode.cn/problems/search-in-a-binary-search-tree/)

```c++
class Solution {
public:
    TreeNode* searchBST(TreeNode* root, int val) {
               stack<TreeNode*>st;
               if(root==nullptr||root->val==val)return root;
               st.push(root);
               TreeNode *p=st.top();
               while(p!=nullptr||!st.empty()){
       
               if(p!=nullptr){st.push(p);p=p->left;}
              else{ 
                 p=st.top();
                 st.pop();
                 if(p->val==val)return p;                  
                 p=p->right;
                }
                   
             }
          return nullptr;
    }
};
```

没用性质干。。。

```c++
class Solution {
public:
    TreeNode* searchBST(TreeNode* root, int val) {
  if (root == NULL || root->val == val) return root;
        TreeNode* result = NULL;
        if (root->val > val) result = searchBST(root->left, val);
        if (root->val < val) result = searchBST(root->right, val);
        return result;
    }
};
```

### [98. 验证二叉搜索树](https://leetcode.cn/problems/validate-binary-search-tree/)

```c++
class Solution {
public:
    bool isValidBST(TreeNode* root) {
            stack<TreeNode*>st;
            if(root==nullptr)return root;
           TreeNode* pre=nullptr;
           TreeNode* p=root;
           while(p!=nullptr||!st.empty()){
            if(p!=nullptr)
            {st.push(p);
            p=p->left;}
           else{p=st.top();
                st.pop();
                if(pre!=nullptr&&p->val<=pre->val){return false;}
                pre=p;
                p=p->right;
           }
           }
           return true;
    }
};
```

中序迭代
