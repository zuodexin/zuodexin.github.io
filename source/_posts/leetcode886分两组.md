---
title: leetcode886分两组
date: 2020-11-22 17:31:45
tags: [leetcode]
---

和是否二分图那道题一样的做法，要注意图需要初始化为无向图。

<!--more-->

```c++
class Solution {
public:
    bool possibleBipartition(int N, vector<vector<int>>& dislikes) {
        vector<vector<int>> adj(N,vector<int>(0));
        vector<int> root(N,0);
        for(int i=0;i<N;i++){
            root[i] = i;
        }
        for(int i=0;i<dislikes.size();i++){
            adj[dislikes[i][0]-1].push_back(dislikes[i][1]-1);
            adj[dislikes[i][1]-1].push_back(dislikes[i][0]-1);
        }
        for(int i=0;i<N;i++){
            int p = find(root,i);
            for(int j=0;j<adj[i].size();j++){
                int q = find(root,adj[i][j]);
                int r = find(root,adj[i][0]);
                // cout<<"p: "<< p << " q: " << q <<" r: "<< r << endl;
                if(p==q) return false;
                else{
                    root[q] = r;
                }
            }
        }
        // cout<<"****"<<endl;
        return true;
    }
    
    int find(vector<int>& root,int i){
        if(root[i]!=i){
            int r = find(root,root[i]);
            root[i] = r;
            return r;
        }else return i;
    }
    
};
```