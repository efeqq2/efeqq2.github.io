---
layout:     post
title:      (leetcode第三天)
subtitle:   (水)
date:       2018-12-01
author:     (作者名)
header-img: img/the-first.png
catalog:   true
tags:
    - 学习
---


### [206. 反转链表](https://leetcode.cn/problems/reverse-linked-list/)

##### 给你单链表的头节点 `head` ，请你反转链表，并返回反转后的链表

```c++
class Solution {
//新建一个头结点，然后用头插法
public:
    ListNode* reverseList(ListNode* head) {
      ListNode*h = new ListNode;
       ListNode*p=head;     
        while(p!=NULL){
            ListNode*t = p;
            p = p->next;
            t->next = h->next;
            h->next = t;
        }

        return h->next;
    }
};
```

头插法

### [203. 移除链表元素](https://leetcode.cn/problems/remove-linked-list-elements/)

```c++
class Solution {
public:
    ListNode* removeElements(ListNode* head, int val) {
      struct ListNode* dummyHead = new ListNode(0, head);
      struct ListNode* temp = dummyHead;
       while (temp->next != NULL) {
            if (temp->next->val == val) {
                temp->next = temp->next->next;
            } else {
                temp = temp->next;
            }
        }
        return dummyHead->next;
    }
    
};
```

遍历

### 



