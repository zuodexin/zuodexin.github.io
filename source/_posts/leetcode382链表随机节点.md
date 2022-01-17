---
title: leetcode382链表随机节点
tags: [leetcode,随机算法]
---

水库抽样，抽取k个，每次迭代以k/i的概率替换，每个被抽中的数字被替换的概率都是1/k


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
    ListNode* head;
public:
    Solution(ListNode* head) {
        this->head = head;
    }
    
    int getRandom() {
        int i=1;
        ListNode* cur = head;
        int ans = cur->val;
        while(cur!=nullptr){
            if(rand()%i++==0){
                ans = cur->val;
            }
            cur = cur->next;
        }
        return ans;
    }
};

/**
 * Your Solution object will be instantiated and called as such:
 * Solution* obj = new Solution(head);
 * int param_1 = obj->getRandom();
 */
```