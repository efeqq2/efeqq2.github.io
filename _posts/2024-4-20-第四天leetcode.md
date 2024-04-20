---
layout:     post
title:      (leetcode第四天学习)
subtitle:   (leetcode学习)
date:       2024-4-20
author:     (pennytask)
header-img: img/the-first.png
catalog:   true
tags:
    - 学习
---

### [19. 删除链表的倒数第 N 个结点](https://leetcode.cn/problems/remove-nth-node-from-end-of-list/)

##### 给你一个链表，删除链表的倒数第 `n` 个结点，并且返回链表的头结点。

```c++
class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
            ListNode *newhead=new ListNode(0,head);
            ListNode *p=head;
            ListNode *pre=newhead;
            if(head->next==NULL)return {};

            for(int i=0;i<n;i++){
                   p=p->next;
            }
            while(p!=nullptr){
                pre=pre->next;
                p=p->next;     
                }          
             pre->next=pre->next->next; 
              
             return newhead->next;
    }
};
```

  双指针，pre->next=pre->next->next;这里不能用pre与他后面节点两个指针，当n等于链表的长度且长度为2时，经过for循环的p已经为空，不进入while循环，所以使用两个指针时，第二个指针不会动，指向head只能依靠pre自己（大概）

### [24. 两两交换链表中的节点](https://leetcode.cn/problems/swap-nodes-in-pairs/)

##### 给你一个链表，两两交换其中相邻的节点，并返回交换后链表的头节点。你必须在不修改节点内部的值的情况下完成本题（即，只能进行节点交换）。

```c++
class Solution {
public:
    ListNode* swapPairs(ListNode* head) {
      if(head==NULL) return {};
       if(head->next==NULL) return head;
       ListNode *dammyhead=new ListNode(0,head);
       ListNode *p=dammyhead->next;
       ListNode *pre=dammyhead;
       while(p!=NULL&&p->next!=NULL){
        ListNode *temp=p->next;
        p->next=temp->next;
        pre->next=temp;
        temp->next=p;
        pre=p;
        p=p->next;
       }
       return dammyhead->next;
    }
};
```

### [面试题 02.07. 链表相交](https://leetcode.cn/problems/intersection-of-two-linked-lists-lcci/)

##### 给你两个单链表的头节点 `headA` 和 `headB` ，请你找出并返回两个单链表相交的起始节点。如果两个链表没有交点，返回 `null` 。

```c++
class Solution {
public:
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
          
    if (headA == NULL or headB == NULL) {
        return NULL;
    }
    ListNode* dummyA = headA;
    ListNode* dummyB = headB;
    int countA = 0;
    int countB = 0;
    while (dummyA != NULL) {
        dummyA = dummyA->next;
        countA++;
    }
    while (dummyB != NULL) {
        dummyB = dummyB->next;
        countB++;
    }
    int diff = 0;
    dummyA = headA;
    dummyB = headB; 
   if (countA > countB) {
        diff = countA - countB;
        for (int i = 0; i < diff; i++) {
            dummyA = dummyA->next;
        }
    } else {
        diff = countB - countA;
        for (int i = 0; i < diff; i++) {
            dummyB = dummyB->next;
        }
    }
  while (dummyA != NULL) {
        if (dummyA == dummyB) {
            return dummyA;
        } else {
            dummyA = dummyA->next;
            dummyB = dummyB->next;
        }
    }
    
    return NULL;

    }
};
```

第二种双指针，情况一：两个链表相交

链表 headA\textit{headA}headA 和 headB\textit{headB}headB 的长度分别是 mmm 和 nnn。假设链表 headA\textit{headA}headA 的不相交部分有 aaa 个节点，链表 headB\textit{headB}headB 的不相交部分有 bbb 个节点，两个链表相交的部分有 ccc 个节点，则有 a+c=ma+c=ma+c=m，b+c=nb+c=nb+c=n。

如果 a=ba=ba=b，则两个指针会同时到达两个链表相交的节点，此时返回相交的节点；

如果 a≠ba \ne ba
\\
=b，则指针 pA\textit{pA}pA 会遍历完链表 headA\textit{headA}headA，指针 pB\textit{pB}pB 会遍历完链表 headB\textit{headB}headB，两个指针不会同时到达链表的尾节点，然后指针 pA\textit{pA}pA 移到链表 headB\textit{headB}headB 的头节点，指针 pB\textit{pB}pB 移到链表 headA\textit{headA}headA 的头节点，然后两个指针继续移动，在指针 pA\textit{pA}pA 移动了 a+c+ba+c+ba+c+b 次、指针 pB\textit{pB}pB 移动了 b+c+ab+c+ab+c+a 次之后，两个指针会同时到达两个链表相交的节点，该节点也是两个指针第一次同时指向的节点，此时返回相交的节点。

情况二：两个链表不相交

链表 headA\textit{headA}headA 和 headB\textit{headB}headB 的长度分别是 mmm 和 nnn。考虑当 m=nm=nm=n 和 m≠nm \ne nm
\\
=n 时，两个指针分别会如何移动：

如果 m=nm=nm=n，则两个指针会同时到达两个链表的尾节点，然后同时变成空值 null\text{null}null，此时返回 null\text{null}null；

如果 m≠nm \ne nm
\\
=n，则由于两个链表没有公共节点，两个指针也不会同时到达两个链表的尾节点，因此两个指针都会遍历完两个链表，在指针 pA\textit{pA}pA 移动了 m+nm+nm+n 次、指针 pB\textit{pB}pB 移动了 n+mn+mn+m 次之后，两个指针会同时变成空值 null\text{null}null，此时返回 null\text{null}null。

​      方法二精髓(个人理解)：相交节点之前的路径两个节点分别走一下，这样加起来就相等了....

也就是<指针a>既走了<链表a>的相交前、后的节点，又走了<链表b>的相交前节点，

<指针b>既走了<链表b>的相交前、后的节点，又走了<链表a>的相交前节点

### [142. 环形链表 II](https://leetcode.cn/problems/linked-list-cycle-ii/)

##### 给定一个链表的头节点  `head` ，返回链表开始入环的第一个节点。 *如果链表无环，则返回 `null`。*

```c++
class Solution {
public:
  ListNode *detectCycle(ListNode *head) {
  ListNode *slow = head, *fast = head;
        while (fast != nullptr) {
            slow = slow->next;
            if (fast->next == nullptr) {
                return nullptr;
            }
            fast = fast->next->next;
            if (fast == slow) {
                ListNode *ptr = head;
                while (ptr != slow) {
                    ptr = ptr->next;
                    slow = slow->next;
                }
                return ptr;
            }
        }
        return nullptr;
    }

```

快慢指针，感觉主要是数学问题



