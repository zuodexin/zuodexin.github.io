---
title: leetcode547朋友圈
date: 2020-11-21 21:21:40
tags: [leetcode]
---

可以用bfs、dfs、和并查集，下面我们用并查集来做，注意：每合并一次朋友圈的数量减1

<!--more-->

```c++
class Solution {
public:
    int findCircleNum(vector<vector<int>>& M) {
        if(M.size()==0) return 0;
        int res = M.size();
        vector<int> root(M.size());
        for(int i=0;i<M.size();i++) root[i] = i;
        for(int i=0;i<M.size();i++){
            for(int j=i;j<M.size();j++){
                if(i==j) continue;
                if(M[i][j]==0) continue;
                int rj = find(root,j);
                int ri = find(root,i);
                if(rj!=ri){
                    res--;
                    root[rj] = ri;
                }
            }
        }
        return res;
    }
    int find(vector<int>& root,int i){
        return root[i]==i?i:find(root,root[i]);
    }
};
```

并查集优化技巧,查询时缩短深度
```c++
int find(vector<int>& root, int i) {
        while (i != root[i]) {
            root[i] = root[root[i]];
            i = root[i];
        }
        return i;
    }
```