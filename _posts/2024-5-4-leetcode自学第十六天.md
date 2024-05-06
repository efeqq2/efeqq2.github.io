---
layout:     post
title:      (leetcode学习第十六天)
subtitle:   (leetcode学习第十六天)
date:       2024-5-6
author:     (pennytask)
header-img: img/the-first.png
catalog:   true
tags:
    - 学习
---


### [101. 对称二叉树](https://leetcode.cn/problems/symmetric-tree/)

```c++
class Solution {

public:

  bool compare(TreeNode* left, TreeNode* right){

   if(left!=nullptr&&right==nullptr)return false;

   else if(left==nullptr&&right!=nullptr)return false;

   else if(left==nullptr&&right==nullptr)return true;

   else if(left!=nullptr&&right!=nullptr&&left->val!=right->val)return false;

   else {

​    return compare(left->left,right->right)&&compare(left->right,right->left);

   }

  }

  

  bool isSymmetric(TreeNode* root) {

​     if (root == NULL) return true;

​    return compare(root->left, root->right);

  }

};
```

### [110. 平衡二叉树](https://leetcode.cn/problems/balanced-binary-tree/)

```C
class Solution {
public:
    int getHeight(TreeNode* node){
        if(node==nullptr)return 0;
        int leftHeight = getHeight(node->left); 
       if (leftHeight == -1) return -1;
       int rightHeight = getHeight(node->right); 
       if (rightHeight == -1) return -1;
       int result;
       if (abs(leftHeight - rightHeight) > 1) {  
        result = -1;
}  else {
          result = 1 + max(leftHeight, rightHeight); 
}

    return result;
    }
    bool isBalanced(TreeNode* root) {
       return getHeight(root) == -1 ? false : true;
    }
};
```

### [404. 左叶子之和](https://leetcode.cn/problems/sum-of-left-leaves/)

```c++
class Solution {
public:
    int sumOfLeftLeaves(TreeNode* root) {
      stack<TreeNode*>st;
      int res=0;
          if(root==nullptr)return 0;
          st.push(root);
          while(!st.empty()){
            TreeNode *p=st.top();
            st.pop();
            if(p->left!=nullptr&&p->left->left==nullptr&&p->left->right==nullptr){
                  res+=p->left->val;
            }
           if(p->left)st.push(p->left);
           if(p->right)st.push(p->right);
          }
          return res;
          
    }
};
```
### [222. 完全二叉树的节点个数](https://leetcode.cn/problems/count-complete-tree-nodes/)

```c++
class Solution {
public:
    int countNodes(TreeNode* root) {
        if (root == nullptr) return 0;
        TreeNode* left = root->left;
        TreeNode* right = root->right;
        int leftDepth = 0, rightDepth = 0; // 这里初始为0是有目的的，为了下面求指数方便
        while (left) {  // 求左子树深度
            left = left->left;
            leftDepth++;
        }
        while (right) { // 求右子树深度
            right = right->right;
            rightDepth++;
        }
        if (leftDepth == rightDepth) {
            return (2 << leftDepth) - 1; // 注意(2<<1) 相当于2^2，所以leftDepth初始为0
        }
        return countNodes(root->left) + countNodes(root->right) + 1;
    }
};
```

用完全二叉树的性质解题，加深对于位运算的使用-1实际上是对二进制进行减法，返回的是十进制数。
