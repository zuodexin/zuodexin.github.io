---
title: leetcode116填充每个节点的下一个右侧节点指针
tags: [leetcode,二叉树]
---

二叉树的非递归层次遍历

```c++
/*
// Definition for a Node.
class Node {
public:
    int val;
    Node* left;
    Node* right;
    Node* next;

    Node() : val(0), left(NULL), right(NULL), next(NULL) {}

    Node(int _val) : val(_val), left(NULL), right(NULL), next(NULL) {}

    Node(int _val, Node* _left, Node* _right, Node* _next)
        : val(_val), left(_left), right(_right), next(_next) {}
};
*/

class Solution {
public:
    Node* connect(Node* root) {
        if(!root) return root;
        Node* head = root;
        root->next = nullptr;
        while(head){
            Node* cur = head;
            while(cur){
                if(cur->left) cur->left->next = cur->right;
                if(cur->right && cur->next) cur->right->next = cur->next->left;
                if(cur->right && !cur->next) cur->right->next = nullptr;
                cur = cur->next;
            }
            head = head->left;
        }
        return root;
    }
};
```