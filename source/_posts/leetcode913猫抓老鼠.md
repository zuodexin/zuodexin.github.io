---
title: leetcode913，猫抓老鼠
tags: [leetcode,动态规划,博弈]
---

```c++
#define MAXN 51

class Solution {
    int dp[MAXN][MAXN][2*MAXN+1];
    vector<vector<int>> graph;
    int priority[2][3]{2,3,1,2,1,3};
public:
    int catMouseGame(vector<vector<int>>& graph) {
        memset(dp,-1,sizeof(dp));
        this->graph = graph;
        int ans = dfs(1,2,0);
        return ans;
    };
    
    // mouse priority: 1,0,2 -> 2,3,1
    // cat priority: 2,0,1 -> 2,1,3
    int chioce=0;
    int dfs(int mouse,int cat,int turn){
        if(turn>=2*graph.size()) return 0;
        if(dp[mouse][cat][turn]!=-1) return dp[mouse][cat][turn];
        if(mouse==0) return 1;
        else if(mouse==cat) return 2;
        else if(turn%2==0){
            int max_score=-1;
            for(int i=0;i<graph[mouse].size();i++){
                int state = dfs(graph[mouse][i],cat,turn+1);
                int score = priority[0][state];
                if(score>max_score){
                    max_score = score;
                    dp[mouse][cat][turn] = state;
                    chioce = graph[mouse][i];
                }
            }
        } else{
            int max_score=-1;
             for(int i=0;i<graph[cat].size();i++){
                if(graph[cat][i]==0) continue;
                int state = dfs(mouse,graph[cat][i],turn+1);
                int score = priority[1][state];
                if(score>max_score){
                    max_score = score;
                    dp[mouse][cat][turn] = state;
                    chioce = graph[cat][i];
                }
            }
        }
        return dp[mouse][cat][turn];
    };
};
```