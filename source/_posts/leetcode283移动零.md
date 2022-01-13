---
title: leetcode移动零
tags: [leetcode,双指针]
---

可以根据本题总结出双指针的解题步骤
1. 双指针的初始化。l指向0，l之前非0，r是l后第一个非零的元素，l和r之间都为0
2. 移动双指针维持约束。l和r元素交换，l+1元素为0，r移动到下一个非0元素


```c++
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        int l=0,r=0,n=nums.size();
        if(n<=1) return;
        while(l<n && nums[l]!=0) l++;
        r = l;
        while(r<n && nums[r]==0) r++;
        while(r<n){
            if(nums[r]==0){
                r++;
                continue;
            }
            swap(nums[l],nums[r]);
            l++;
            r++;
        }
    }
};
```