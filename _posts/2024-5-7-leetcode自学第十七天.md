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

