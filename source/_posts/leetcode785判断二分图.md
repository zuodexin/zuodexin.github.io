---
title: leetcode785判断二分图
date: 2020-11-21 20:26:27
tags:
---

这道题可以用dfs、bfs，并查集都可以做，下面的代码用是并查集实现的


<!--more-->


```c++
class Solution {
public:
    bool isBipartite(vector<vector<int>>& graph) {
        vector<int> root(graph.size());
        for(int i=0;i<graph.size();i++) root[i] =i;
        for(int i=0;i<graph.size();i++){
            if(graph[i].size()==0) continue;
            int p = find(root,i);
            int q = find(root,graph[i][0]);
            if(p==q) return false;
            for(int j =1;j<graph[i].size();j++){
                int r = find(root,graph[i][j]);
                if(r==p) return false;
                else root[graph[i][j]] = q;
            }
        }
        return true;
    }
    
    int find(vector<int>& root,int i){
        return root[i]==i? i:find(root, root[i]);
    } 
};
```