---
title: leetcode464我能赢吗
date: 2020-11-22 10:41:02
tags: [leetcode,dfs,状态压缩]
---


```c++
class Solution {
public:
    bool canIWin(int maxChoosableInteger, int desiredTotal) {
        bool memo[(1<<20)-1]{0};
        if(maxChoosableInteger*(maxChoosableInteger+1)/2 < desiredTotal){
            return false;
        }
        int state=0;
        int cur = 0;
        return dfs(memo,state,cur,maxChoosableInteger,desiredTotal);
    }
    
    bool dfs(bool memo[],int state,int cur,int n,int target){
        for(int i=1;i<=n;i++){
            if(state & (1<<(i-1))) continue;
            state |= 1<<(i-1);
            cur += i;
            if(cur>=target) return true;
            //else if(!dfs(memo,state,cur,n,target)){
            else if(!memo[state]&&!dfs(memo,state,cur,n,target)){
                return true;
            }
            memo[state] = true;
            cur -= i;
            state ^= 1<<(i-1);
        }
        return false;
    }
};
```