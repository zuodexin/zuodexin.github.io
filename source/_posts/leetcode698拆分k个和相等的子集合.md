---
title: leetcode698拆分k个和相等的子集合
date: 2020-11-17 21:56:39
tags: [leetcode]
---

回溯法求解

<!--more-->

```c++
class Solution {
public:
    bool canPartitionKSubsets(vector<int>& nums, int k) {
        if(nums.size()<k){
            return false;
        }
        int sum=0;
        for(int i=0;i<nums.size();i++){
            sum+=nums[i];
        }
        if(sum%k!=0){
            return false;
        }
        vector<int> subsets(k,0);
        vector<bool> picked(nums.size(),false);
        std::sort(nums.begin(),nums.end(),std::greater<int>());
        return helper(nums,k,subsets,picked,sum/k);
    }
    bool helper(vector<int>& nums,int k,vector<int>&subsets,vector<bool>&picked,int s){
        for(int i=0;i<nums.size();i++){
            if(!picked[i]){
                for(int j=0;j<subsets.size();j++){
                    if(subsets[j]+nums[i]<=s){
                        picked[i] = true;
                        subsets[j] += nums[i];
                        // printf("nums[%d]:%d subsets[%d]:%d\n",i,nums[i],j,subsets[j]);
                        if(helper(nums,k,subsets,picked,s))
                            return true;
                        else{
                            picked[i] = false;
                            subsets[j] -= nums[i];
                        }
                    }
                }
                return false;
            }
        }
        return true;
    }
};
```