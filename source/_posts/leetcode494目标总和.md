---
title: leetcode494目标总和
date: 2020-11-22 11:22:15
tags: [leetcode]
---


动态规划

<!--more-->


```c++
class Solution {
public:
    int findTargetSumWays(vector<int>& nums, int S) {
        if(abs(S)>1000) return 0;
        int dp[21][2001]{0};
        dp[0][0+1000] = 1;
        for(int i=0;i<nums.size();i++){
            for(int j=0;j<2001;j++){
                dp[i+1][min(j+nums[i],2000)] += dp[i][j];
                dp[i+1][max(j-nums[i],0)] += dp[i][j];
            }
        }
        return dp[nums.size()][S+1000];
    }
};
```