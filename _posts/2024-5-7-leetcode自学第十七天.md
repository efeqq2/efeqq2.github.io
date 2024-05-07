---
layout:     post
title:      (leetcode学习第十七天)
subtitle:   (leetcode学习第十七天)
date:       2024-5-7
author:     (pennytask)
header-img: img/wallhaven-l8v3ey.png
catalog:   true
tags:
    - 学习
---

### [513. 找树左下角的值](https://leetcode.cn/problems/find-bottom-left-tree-value/)

```c++
class Solution {
public:
    int findBottomLeftValue(TreeNode* root) {
            queue<TreeNode*>que;
            int res;
            que.push(root);
            while(!que.empty()){
                int size=que.size();
                for(int i=0;i<size;i++){
                    TreeNode *p=que.front();
                    que.pop();
                    if(i==0){
                        res=p->val;
                    }
                  if(p->left!=nullptr)que.push(p->left);
                  if(p->right!=nullptr)que.push(p->right);
                }
            }
            return res;
    }
};
```

### [112. 路径总和](https://leetcode.cn/problems/path-sum/)

```c++
class Solution {
public:
    bool hasPathSum(TreeNode* root, int targetSum) {
        stack<TreeNode*> st;
        if (root == nullptr) return false;
        st.push(root);

        while (!st.empty()) {
            TreeNode* p = st.top();
            st.pop();

            if (p->left == nullptr && p->right == nullptr && p->val == targetSum) {
                return true;
            }

            if (p->right != nullptr) {
                p->right->val += p->val;
                st.push(p->right);
            }

            if (p->left != nullptr) {
                p->left->val += p->val;
                st.push(p->left);
            }
        }

        return false;
    }
};
```

直接加上去就避免了使用变量记录当前数据时需要回溯或者需要使用pair的情况
### [106. 从中序与后序遍历序列构造二叉树](https://leetcode.cn/problems/construct-binary-tree-from-inorder-and-postorder-traversal/)

```c++
class Solution {
private:
  
    TreeNode* traversal (vector<int>& inorder, int inorderBegin, int inorderEnd, vector<int>& postorder, int postorderBegin, int postorderEnd) {
        if (postorderBegin == postorderEnd) return NULL;
        int rootValue = postorder[postorderEnd - 1];
         TreeNode* root = new TreeNode(rootValue);
               if (postorderEnd - postorderBegin == 1) return root;
                 int delimiterIndex;
        for (delimiterIndex = inorderBegin; delimiterIndex < inorderEnd; delimiterIndex++) {
            if (inorder[delimiterIndex] == rootValue) break;
        }
          int leftInorderBegin = inorderBegin;
        int leftInorderEnd = delimiterIndex;
         int rightInorderBegin = delimiterIndex + 1;
        int rightInorderEnd = inorderEnd;
          int leftPostorderBegin =  postorderBegin;
        int leftPostorderEnd = postorderBegin + delimiterIndex - inorderBegin; // 终止位置是 需要加上 中序区间的大小size
        // 右后序区间，左闭右开[rightPostorderBegin, rightPostorderEnd)
        int rightPostorderBegin = postorderBegin + (delimiterIndex - inorderBegin);
        int rightPostorderEnd = postorderEnd - 1; // 排除最后一个元素，已经作为节点了
         root->left = traversal(inorder, leftInorderBegin, leftInorderEnd,  postorder, leftPostorderBegin, leftPostorderEnd);
        root->right = traversal(inorder, rightInorderBegin, rightInorderEnd, postorder, rightPostorderBegin, rightPostorderEnd);

        return root;
}
public:
    TreeNode* buildTree(vector<int>& inorder, vector<int>& postorder) {
 if (inorder.size() == 0 || postorder.size() == 0) return NULL;
        // 左闭右开的原则
        return traversal(inorder, 0, inorder.size(), postorder, 0, postorder.size());
    }
    
};
```

[代码随想录 (programmercarl.com)](https://programmercarl.com/0106.从中序与后序遍历序列构造二叉树.html#思路)

需要反复观看。
