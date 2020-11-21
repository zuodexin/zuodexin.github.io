---
title: leetcode863距离为K的所有二叉树节点
date: 2020-11-21 22:53:46
tags: [leetcode]
---

需要熟悉二叉树中的距离概念，这道题可以作为一道很好的递归、回溯练习题。

<!--more-->

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    vector<int> distanceK(TreeNode* root, TreeNode* target, int K) {
        vector<int> res;
        if(root==NULL) return res;
        core(root,target,K,res);
        // cout<< "****"<< endl;
        return res;
    }
    
    void core(TreeNode* root, TreeNode* target, int K,vector<int>& nums){
        if(root==NULL) return;
        if(root->val==target->val){
            downwardK(target,K,nums);
            return;
        }
        int rd = find(root->right,target)+1;
        int ld = find(root->left,target)+1;
        // cout<<"rd: "<< rd << " ld: "<< ld <<" K: "<<K<< endl;
        if(rd==0){
            if(K==ld){
                nums.push_back(root->val);
            }
            downwardK(root->right,K-ld-1,nums);
            core(root->left,target,K,nums);
        }else if(ld==0){
            if(K==rd){
                nums.push_back(root->val);
            }
            downwardK(root->left,K-rd-1,nums);
            core(root->right,target,K,nums);
        }
    }
    
    void downwardK(TreeNode* root, int k,vector<int>& nums){
        if(root==NULL || k<0 ) return ;
        // cout<<"root "<< root->val << "k: "<<k<<endl;
        if(k==0){
            nums.push_back(root->val);
            return;
        }
        downwardK(root->left,k-1,nums);
        downwardK(root->right,k-1,nums);
    }
    
    int find(TreeNode* root, TreeNode* target){
        if(root==NULL) return -1;
        if(root->val==target->val) return 0;
        int rd = find(root->right,target);
        int ld = find(root->left,target);
        if(rd!=-1){
            return rd+1;
        }else if(ld!=-1){
            return ld+1;
        }else return -1;
    }
};
```