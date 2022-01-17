---
title: leetcode19删除链表中倒数第n个节点
tags: [leetcode,双指针]
---
学会在链表头部加上一个空节点，有关链表的代码会简化很多。

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        ListNode dummy = ListNode(0,head);
        ListNode* l=&dummy,*r=&dummy;
        for(int i=0;i<n;i++){
            if(r)r = r->next;
            else return head; //n > list size
        }
        while(r->next){
            r = r->next;
            l = l->next;
        }
        l->next = (l->next)?l->next->next:nullptr;
        return dummy.next;
    }
};
```