---
title: leetcode477全部汉明距离
date: 2020-11-22 10:41:02
tags: [leetcode]
---

分别统计每一位上0，1的个数，这一位产生的汉明距离就是二者的乘积

<!--more-->

```c++
class Solution {
public:
    int totalHammingDistance(vector<int>& nums) {
        int bit = 32;
        int sum = 0;
        for(int i=0;i<bit;i++){
            int cnt_0 = 0, cnt_1 = 0;
            for(int j=0;j<nums.size();j++){
                int num = nums[j];
                if (num & ( 1 << i )){
                    cnt_1++;
                }else{
                    cnt_0++;
                }
            }
            sum += cnt_0*cnt_1;
        }
        return sum;
    }
};
```