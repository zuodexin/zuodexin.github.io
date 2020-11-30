---
title: leetcode1020enclave的数量
date: 2020-11-25 21:33:34
tags:[leetcode]
---

暴力dfs，更简单的是只在边界上dfs

<!--more-->

```c++
typedef pair<int,int> Point;

class Solution {
    vector<vector<int>>d{{0,1},{1,0},{0,-1},{-1,0}};
public:
    int numEnclaves(vector<vector<int>>& A) {
        if(A.size()==0||A[0].size()==0) return 0;
        vector<vector<bool>> counted(A.size(),vector<bool>(A[0].size(),false));
        int sum = 0;
        for(int i=0;i<A.size();i++){
            for(int j=0;j<A[0].size();j++){
                if(counted[i][j]) continue;
                // cout<<i<<" "<<j<<endl;
                int area = dfs(A,i,j,counted);
                if(area==-1) continue;
                sum+=area;
            }
        }
        return sum;
    }
    int dfs(vector<vector<int>>& A,int x,int y,vector<vector<bool>>&counted){
        if(x<0||x>=A.size()||y<0||y>=A[0].size()) return -1;
        if(A[x][y]==0) return 0;
        if(counted[x][y]) return 0;
        counted[x][y] = true;
        int area = 1;
        bool f= true;
        for(int i=0;i<d.size();i++){
            int t = dfs(A,x+d[i][0],y+d[i][1],counted);
             if(t==-1) {
                f=false;
            }
            else{
                area+=t;
            }
        }
        return f?area:-1;
    }
};
```