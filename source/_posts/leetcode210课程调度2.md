---
title: leetcode210课程调度2
date: 2020-11-22 16:33:49
tags: [leetcode]
---

这道题其实就是拓补排序，拓补排序可以用dfs做，也可以用入度优先队列来做,注意检测是否存在环。

<!--more-->

```c++
class Solution {
public:
    vector<int> findOrder(int numCourses, vector<vector<int>>& prerequisites) {
        vector<int> in_stack(numCourses,0);
        vector<vector<int>> adj(numCourses,vector<int>(0));
        stack<int> s;
        vector<int> res;
        vector<bool> visited(numCourses,false);
        for(int i=0;i< prerequisites.size();i++){
            adj[prerequisites[i][1]].push_back(prerequisites[i][0]);
        }
        for(int i=0;i<numCourses;i++){
            if(!dfs(in_stack,adj,i,s,visited)) return vector<int>();
        }
        while(!s.empty()){
            res.push_back(s.top());
            s.pop();
        }
        return res;
    }
    
    bool dfs(vector<int>& in_stack,vector<vector<int>>& adj,int node,stack<int>& s,vector<bool>& visited){
        if(visited[node]) return false;
        if(in_stack[node]) return true;
        in_stack[node] =  true;
        visited[node] = true;
        for(int i = 0 ;i < adj[node].size();i++){
            if(!dfs(in_stack,adj,adj[node][i],s,visited)){
                visited[node] = false;
                return false;
            }
        }
        s.push(node);
        visited[node] = false;
        return true;
    }
};
```
