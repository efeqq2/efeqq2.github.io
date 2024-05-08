---
layout:     post
title:      (leetcode自学)
subtitle:   (leetcode自学)
date:       2024-5-8
author:     (pennytask)
header-img: wallhaven-l8v3ey.png
catalog:   true
tags:
    - 学习
---

### [73. 矩阵置零](https://leetcode.cn/problems/set-matrix-zeroes/)

给定一个 `*m* x *n*` 的矩阵，如果一个元素为 **0** ，则将其所在行和列的所有元素都设为 **0** 。请使用 **[原地](http://baike.baidu.com/item/原地算法)** 算法**。**

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/08/17/mat1.jpg)

```
输入：matrix = [[1,1,1],[1,0,1],[1,1,1]]
输出：[[1,0,1],[0,0,0],[1,0,1]]
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2020/08/17/mat2.jpg)

```
输入：matrix = [[0,1,2,0],[3,4,5,2],[1,3,1,5]]
输出：[[0,0,0,0],[0,4,5,0],[0,3,1,0]]
```

```c++
class Solution {
public:
    void setZeroes(vector<vector<int>>& matrix) {
              int m=matrix.size();
              int n=matrix[0].size();
              vector<int>row(m),col(n);
              for(int i=0;i<m;i++){
                for(int j=0;j<n;j++){
                    if(matrix[i][j]==0){row[i]=col[j]=true;}
                }
              }
               for(int i=0;i<m;i++){
                for(int j=0;j<n;j++){
               if(row[i]||col[j]){matrix[i][j]=0;}
                }}
    }
};
```

使用标记数组，将行和列设为标记，当需要更改时将标记数组里变身为true，再遍历一次行或列正在标记中为true的将值改为0.、

### [138. 随机链表的复制](https://leetcode.cn/problems/copy-list-with-random-pointer/)

```c++
class Solution {
public:
    Node* copyRandomList(Node* head) {
        if(head==NULL)return NULL;
        Node* cur=head;
        unordered_map<Node*,Node*>map;
        while(cur!=NULL){
            map[cur]=new Node(cur->val);
            cur=cur->next;
        }
        cur=head;
        while(cur!=NULL){
            map[cur]->next=map[cur->next];
            map[cur]->random=map[cur->random];
            cur=cur->next;
        }
        return map[head];
    }
};
```

理解哈希表。成为哈希表。超越哈希表。哈希表的实质就是储存一些键值对，map[cur]实际上指向的是<first，second>中的second，

 while(cur!=NULL){
            map[cur]=new Node(cur->val);
            cur=cur->next;
        }

复制了一遍整个链表，并且跟原本的链表组成一对储存在哈希表中，接下来通过对second（新链表）进行指针操作来复制链表 map[cur]->next=map[cur->next];map[cur->next]指向的是新链表，但是是通过旧链表来映射到新链表，cur本身就是node类型的节点，不要跟vector弄混淆

  题目也可以由另一种方法，不使用哈希表，而是直接在原链表的每个节点后面再复制一个自己，然后再遍历一次使他们指向应当指向的节点，再遍历一次进行拆分，留下新链表
