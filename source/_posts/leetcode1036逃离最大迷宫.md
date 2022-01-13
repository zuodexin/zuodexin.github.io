---
title: leetcode 逃离最大迷宫
tags: [leetcode,bfs]
---
有限步数的广度优先搜索，其中包含的非障碍位置的数量为：$\frac{n(n-1)}{2}$

```c++
#define GSIZE 999999

struct Pos{
    int x;
    int y;
    Pos(int x,int y):x(x),y(y){};
    bool operator < (const Pos& b) const {
        if(x==b.x) return y<b.y;
        return x<b.x;
    };
    bool operator == (const Pos& b) const{
        return x==b.x && y==b.y;
    };
};


class Solution {
    int dir[4][2] = {{0,1},{1,0},{0,-1},{-1,0}};
public:
    bool isEscapePossible(vector<vector<int>>& blocked, vector<int>& source, vector<int>& target) {
        set<Pos> blk;
        for(int i=0;i<blocked.size();i++){
            blk.insert(Pos(blocked[i][0],blocked[i][1]));
        }
        Pos src(source[0],source[1]),tgt(target[0],target[1]);
        bool b1 = bfs(blk,src,tgt);
        bool b2 = bfs(blk,tgt,src);
        //cout<<b1<<b2<<endl;
        return b1&&b2;
    }

    bool bfs(set<Pos>& blk,Pos& source,Pos& target){
        queue<Pos> q;
        set<Pos> visited;
        q.push(source);
        visited.insert(source);
        int n=blk.size();
        int cnt=0;
        while(!q.empty()){
            Pos t = q.front();
            q.pop();
            if(t==target) return true;
            cnt++;
            if(cnt>(n*(n-1))/2){
                return true;
            }
            for(int i=0;i<4;i++){
                int dx=dir[i][0],dy=dir[i][1];
                Pos np = Pos(t.x+dx,t.y+dy);
                if(np.x<=GSIZE && np.x>=0 && np.y<=GSIZE && np.y>=0 && !visited.count(np) && !blk.count(np)){
                    q.push(np);
                    visited.insert(np);
                }
            }
        }
        return false;
    }
};
```