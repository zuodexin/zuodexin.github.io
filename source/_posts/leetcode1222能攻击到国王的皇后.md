---
title: leetcode1222能攻击到国王的皇后
date: 2020-11-21 19:11:26
tags: [leetcode]
---

有多种解法，一种是在地图上以国王为中心在地图上遍历；另一种是遍历皇后数组，更新最过滤掉被挡住的皇后，这种在皇后比较少的情况下更快

<!--more-->

```c++
class Solution {
public:
    vector<vector<int>> queensAttacktheKing(vector<vector<int>>& queens, vector<int>& king) {
        vector<vector<int>> direction = {
            {0,-1},
            {-1,-1},
            {-1,0},
            {-1,1},
            {0,1},
            {1,1},
            {1,0},
            {1,-1},
        };
        set<std::pair<int,int>> q_set;
        int x_max = king[0],y_max=king[1];
        for(int i=0;i<queens.size();i++){
            q_set.insert(std::make_pair(queens[i][0],queens[i][1]));
            x_max = max(x_max,queens[i][0]);
            y_max = max(y_max,queens[i][1]);
        }
        vector<vector<int>> attack;
        for(int i=0;i<direction.size();i++){
            vector<int> delta = direction[i];
            for(int step=1;;step++){
                int x = king[0]+delta[0]*step;
                int y = king[1]+delta[1]*step;
                if(x<0 || x>x_max || y<0 || y>y_max){
                    break;
                }
                pair<int,int> p = std::make_pair(x,y);
                if(q_set.find(p)!=q_set.end()){
                    vector<int> t;
                    t.push_back(x);
                    t.push_back(y);
                    attack.push_back(t);
                    break;
                }
            }
        }
        return attack;
    }
};
```