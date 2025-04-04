---
layout:     post
title:      (leetcode第十五天)
subtitle:   (leetcode第十五天)
date:       2024-5-4
author:     (pennytask)
header-img: img/the-first.png
catalog:   true
tags:
    - 学习
---


### 二叉树层次遍历

```c++
class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        queue<TreeNode*>que;
        vector<vector<int>>res;
        if(root!=nullptr) que.push(root);
        while(!que.empty()){
           int size = que.size();
            vector<int> vec;
            for(int i=0;i<size;i++){
                TreeNode *node=que.front();
                  que.pop();
                vec.push_back(node->val);
               if (node->left) que.push(node->left);
                if (node->right) que.push(node->right);
            }
             res.push_back(vec);
        }
        return res;
    }
};
```

### n叉树层次遍历

```c++
class Solution {
public:
    vector<vector<int>> levelOrder(Node* root) {
        if(root==NULL){
            return {};
        }
        queue<Node*>que;
        vector<vector<int>>ans;
        que.push(root);
        while(!que.empty()){
            int size=que.size();
            vector<int>res;
            for(int i=0;i<size;i++){
                Node *p=que.front();
                res.push_back(p->val);
                que.pop();
               for(Node* child:p->children){
                que.push(child);
               }
            }
            ans.push_back(res);
        }
        return ans;
    }
};
```

### [515. 在每个树行中找最大值](https://leetcode.cn/problems/find-largest-value-in-each-tree-row/)

```c++
class Solution {
public:
    vector<int> largestValues(TreeNode* root) {
      vector<int>res;
      if(root==nullptr)return res;
      queue<TreeNode*>que;
      que.push(root);
      while(!que.empty()){
        int size=que.size();
        int num=numeric_limits<int>::min();
        for(int i=0;i<size;i++){
         TreeNode *p=que.front();
         que.pop();
         if(p->val>num)num=p->val;
         if(p->left!=nullptr)que.push(p->left);
         if(p->right!=nullptr)que.push(p->right);
        }
        res.push_back(num);
      }
      return res;
    }
};
```

- [107.二叉树的层次遍历II(opens new window)](https://leetcode.cn/problems/binary-tree-level-order-traversal-ii/) 完成
- [199.二叉树的右视图(opens new window)](https://leetcode.cn/problems/binary-tree-right-side-view/)完成
- [637.二叉树的层平均值(opens new window)](https://leetcode.cn/problems/average-of-levels-in-binary-tree/)完成
- ### [116. 填充每个节点的下一个右侧节点指针](https://leetcode.cn/problems/populating-next-right-pointers-in-each-node/)

```c++
class Solution {
public:
    Node* connect(Node* root) {
        queue<Node*>que;
        if(root==NULL)return root;
        que.push(root);
        while(!que.empty()){
         
         int size=que.size();
        
         for(int i=0;i<size;i++){
            Node* q=que.front();
            if(i<size-1){
                 que.pop();
                 q->next=que.front();
            }
            else{
                que.pop();
                q->next==NULL;}
            if(q->left!=NULL)que.push(q->left);
            if(q->right!=NULL)que.push(q->right);
         }
        }
        return root;
        
    }
};
```

  不需要两个指针，出队列的只要不是最后一个节点，指向队首就行了。

##### [104. 二叉树的最大深度](https://leetcode.cn/problems/maximum-depth-of-binary-tree/)  完成

##### [111. 二叉树的最小深度 ](https://leetcode.cn/problems/minimum-depth-of-binary-tree/) 完成 层次遍历 :当左右孩子都没有时候直接返回


