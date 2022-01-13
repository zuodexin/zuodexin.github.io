---
title: leetcode283轮转数组
tags: [leetcode,数学]
---

```c++
class Solution {
public:
    void rotate(vector<int>& nums, int k) {
        int n = nums.size();
        vector<int> ans(n,0);
        k = k%n;
        for(int i=0;i<n;i++){
            ans[i] = nums[(i-k+n)%n];
        }
        for(int i=0;i<n;i++){
            nums[i] = ans[i];
        }
    }
};
```