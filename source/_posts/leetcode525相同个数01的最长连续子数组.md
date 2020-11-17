---
title: leetcode525相同个数01的最长连续子数组
date: 2020-11-17 22:53:39
tags: [leetcode]
---

维护变量count，遇到0减1，遇到1加一，记录遇到count的最早位置，下次遇到后计算长度，
画个折线图就能理解为什么这两个位置间的01个数相等。


扩展一下，以后遇到这种相等的可以考虑一下这种折线图的解法。

<!--more-->
```c++
class Solution {
public:
    int findMaxLength(vector<int>& nums) {
        std::unordered_map<int,int> m;
        m.insert({0,-1});
        int count = 0 ;
        int maxlen = 0;
        for(int i=0;i<nums.size();i++){
            count += nums[i]==1?1:-1;
            if(m.find(count)!=m.end()){
                maxlen = std::max(maxlen,i-m[count]);
            }else{
                m.insert({count,i});
            }
        }
        return maxlen;
    }
};
```