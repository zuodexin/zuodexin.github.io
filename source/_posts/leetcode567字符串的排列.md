---
title: leetcode567字符串的排列
tags: [leetcode,滑动窗口]
---

学会memcmp的使用，返回0表示相等，按照数组的字典顺序排列，字符数组的每个元素按ascii码进行比较

```c++
class Solution {
public:
    bool checkInclusion(string s1, string s2) {
        if(s2.size()<s1.size()) return false;
        int m1[26]{0},m2[26]{0};
        for(int i=0;i<s1.size();i++){
            m1[s1[i]-'a']++;
        }
        int w=s1.size();
        for(int i=0;i<w;i++){
            m2[s2[i]-'a']++;
        }
        for(int i=w;i<s2.size();i++){
            //cout<<s2[i]<<","<<m2[s2[i]-'a']<<","<<sizeof(m1)<<endl;
            if(!memcmp(m1,m2,sizeof(m1))) return true;
            m2[s2[i]-'a']++;
            m2[s2[i-w]-'a']--;
        }
        return !memcmp(m1,m2,sizeof(m1));
    }
};
```