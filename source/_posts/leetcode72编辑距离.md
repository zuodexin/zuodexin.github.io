
---
title: leetcode72，编辑距离
tags: [leetcode,动态规划]
---


```c++


// dp[i][j] = min(dp[i-1]dp[j-1]如果相等,dp[i-1][j]+1,dp[i][j-1]+1,dp[i-1]dp[j-1]+1)


class Solution {
public:
    bool oneEditAway(string first, string second) {
        int distance = editDistance(first,second);
        //cout<<distance<<endl;
        return distance<=1;
    }
    int editDistance(string first,string second){
        vector<vector<int>> dp(first.size()+1,vector<int>(second.size()+1,0));
        for(int i=0;i<=first.size();i++){
            for(int j=0;j<=second.size();j++){
                if (i==0 && j==0){
                    dp[i][j] = 0;
                }else if (i==0){
                    dp[i][j] = dp[i][j-1]+1;
                }else if(j==0){
                    dp[i][j] = dp[i-1][j]+1;
                }else{
                    dp[i][j] = min(min(dp[i-1][j]+1,dp[i][j-1]+1),dp[i-1][j-1]+1);
                }
                if(i>0&& j>0&& first[i-1]==second[j-1]){
                    dp[i][j] = min(dp[i][j],dp[i-1][j-1]);
                }
            }
        }
        return dp[first.size()][second.size()];
    }
};

```