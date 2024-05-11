---
layout:     post
title:      (leetcode学习第二十天)
subtitle:   (leetcode学习第二十天)
date:       2024-5-11
author:     (pennytask)
header-img: img/
catalog:   true
tags:
    - 学习
---
### [235. 二叉搜索树的最近公共祖先](https://leetcode.cn/problems/lowest-common-ancestor-of-a-binary-search-tree/)

```c++
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
         int small=min(p->val,q->val);
         int big=max(p->val,q->val);
         if(root->val<small)return lowestCommonAncestor(root->right,p,q);
         if(root->val>big)return lowestCommonAncestor(root->left,p,q);
          return root;
    }
};
```

root比小的小，祖先在右子树上，比大的大，在左子树上，比一个大一个小root就是祖先。

### [701. 二叉搜索树中的插入操作](https://leetcode.cn/problems/insert-into-a-binary-search-tree/)

```c++
class Solution {
public:
    TreeNode* insertIntoBST(TreeNode* root, int val) {
           if(root==nullptr)return new TreeNode(val);
            if (root->val > val) root->left = insertIntoBST        (root->left, val);
            if (root->val < val) root->right = insertIntoBST(root->right, val);
       return root;
    }
};
```

### [450. 删除二叉搜索树中的节点](https://leetcode.cn/problems/delete-node-in-a-bst/)

```c++
class Solution {
public:
    TreeNode* deleteNode(TreeNode* root, int key) {
        if (root == nullptr) return root;
        if (root->val == key) {

    if (root->left == nullptr) return root->right;

    else if (root->right == nullptr) return root->left;

    else {
        TreeNode* cur = root->right; 
        while(cur->left != nullptr) {
            cur = cur->left;
        }
        cur->left = root->left; 
        root = root->right;     
        return root;
    }
}
       if (root->val > key) root->left = deleteNode(root->left, key);
       if (root->val < key) root->right = deleteNode(root->right, key);
 return root;
    }
};
```

  递归，第一种情况：没找到删除的节点，遍历到空节点直接返回了

- 找到删除的节点
  - 第二种情况：左右孩子都为空（叶子节点），直接删除节点， 返回NULL为根节点
  - 第三种情况：删除节点的左孩子为空，右孩子不为空，删除节点，右孩子补位，返回右孩子为根节点
  - 第四种情况：删除节点的右孩子为空，左孩子不为空，删除节点，左孩子补位，返回左孩子为根节点
  - 第五种情况：左右孩子节点都不为空，则将删除节点的左子树头结点（左孩子）放到删除节点的右子树的最左面节点的左孩子上，返回删除节点右孩子为新的根节点。

