---
title: leetcode1530好叶子节点对的数量
tags: [leetcode,树,DFS]
---
左右需返回不同深度叶子节点的统计个数，超过distance的需去除
```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    int countPairs(TreeNode* root, int distance) {
        map<int,int> level_cnt;
        int ans = 0;
        dfs(root,distance,level_cnt,ans);
        return ans;
    }

    void dfs(TreeNode* root,int distance,map<int,int>& level_cnt,int& ans){
        if(root->left==nullptr && root->right==nullptr){
            level_cnt[0] = 1;
        }
        map<int,int> lc,rc;
        if(root->left!=nullptr) dfs(root->left,distance,lc,ans);
        if(root->right!=nullptr) dfs(root->right,distance,rc,ans);
        for(auto it = lc.begin();it!=lc.end();it++){
            int depth = it->first+1;
            int l_cnt = it->second;
            if(depth>=distance) break;
            level_cnt[depth] = l_cnt;
            int r_cnt = 0;
            auto rb = rc.upper_bound(distance-depth-1);
            for(auto jt=rc.begin();jt!=rb;jt++){
                r_cnt += jt->second;
            }
            //cout<<"ld"<<depth<<",lcnt:"<<l_cnt<<",rd:"<<rb->first<<",rcnt:"<<r_cnt<<endl;
            ans += l_cnt*r_cnt;
        }
        for(auto it = rc.begin();it!=rc.end();it++){
            int depth = it->first+1;
            if(depth>=distance-1) break;
            level_cnt[depth] += it->second;
        }
    }
};
```