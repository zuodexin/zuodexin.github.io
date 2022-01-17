---
title: leetcode
tags: [leetcode,滑动窗口]
---


```c++
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        int ans=0;
        unordered_set<int> st;
        int l=0;
        for(int i=0;i<s.size();i++){
            while(st.count(s[i]))st.erase(s[l++]);
            st.insert(s[i]);
            if(st.size()>ans) ans = st.size();
        }
        return ans;
    }
};
```