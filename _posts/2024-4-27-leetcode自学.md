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
### [148. 排序链表](https://leetcode.cn/problems/sort-list/)

##### 给你链表的头结点 `head` ，请将其按 **升序** 排列并返回 **排序后的链表** 。 `O(n log n)` 时间复杂度和常数级空间复杂度。

```c++
class Solution {
public:
    ListNode* sortList(ListNode* head) {         
           return sortList(head, nullptr);
    }
     ListNode* sortList(ListNode* head, ListNode* tail) {   //重载，使用快慢指针分割链表，当一段里只有一个节点时返回自己，当链表里有两个节点时断开返回头部，其他情况下用fast，slow分割
        if (head == nullptr) {
            return head;
        }
        if (head->next == tail) {
            head->next = nullptr;
            return head;
        }
        ListNode* slow = head, *fast = head;
        while (fast != tail) {
            slow = slow->next;
            fast = fast->next;
            if (fast != tail) {
                fast = fast->next;
            }
        }
        ListNode* mid = slow;
        return merge(sortList(head, mid), sortList(mid, tail));    //递归分割并排序
    }
         ListNode* merge(ListNode* head1, ListNode* head2) {  //归并排序
        ListNode* dummyHead = new ListNode(0);
        ListNode* temp = dummyHead, *temp1 = head1, *temp2 = head2;
        while (temp1 != nullptr && temp2 != nullptr) {
            if (temp1->val <= temp2->val) {
                temp->next = temp1;
                temp1 = temp1->next;
            } else {
                temp->next = temp2;
                temp2 = temp2->next;
            }
            temp = temp->next;
        }
        if (temp1 != nullptr) {
            temp->next = temp1;
        } else if (temp2 != nullptr) {
            temp->next = temp2;
        }
        return dummyHead->next;
    }


};
```

  由时间复杂度想到二分法，再由二分法想到归并排序，递归的终止条件是链表的节点个数小于或等于 111，即当链表为空或者链表只包含 1 个节点时，不需要对链表进行拆分和排序。

### [74. 搜索二维矩阵](https://leetcode.cn/problems/search-a-2d-matrix/)

给你一个满足下述两条属性的 `m x n` 整数矩阵：

- 每行中的整数从左到右按非严格递增顺序排列。
- 每行的第一个整数大于前一行的最后一个整数。

给你一个整数 `target` ，如果 `target` 在矩阵中，返回 `true` ；否则，返回 `false` 。

 

```c++
class Solution {
public:
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
            int  n=matrix[0].size();//列
            int  m= matrix.size(); //行
            int i=0,j=n-1;
            while(i<m&&j>=0){
                if(matrix[i][j]==target) return true;
                else if(matrix[i][j]<target) i++;
                else if(matrix[i][j]>target)  j--;
            }
            return false;
        
    }
};
```

从右上角开始遍历，比右上角大必定不在此行，比右上角小必定不在此列。


