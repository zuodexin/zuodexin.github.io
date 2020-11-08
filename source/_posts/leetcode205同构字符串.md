---
title: leetcode205同构字符串
date: 2020-11-08 16:28:52
tags:
---


做这道题要先理解什么是同构字符串，以及字符的替换规则

用两个unordered_map来保存映射关系

注意maker_pair中的类型为引用类型

```
class Solution {
public:
    bool isIsomorphic(string s, string t) {
        if(s.length()!=t.length()){
            return false;
        }
        if(s.length()==0) return true;
        unordered_map<char,char> replaced;
        unordered_map<char,char> reversed; 
        for(int i=0;i<s.length();i++){
            if(replaced.find(s[i])!=replaced.end()){
                if(replaced[s[i]]!=t[i]){
                    return false;
                }
            }else{
                if(reversed.find(t[i])!=reversed.end()){
                    return false;
                }else{
                    replaced.insert(std::make_pair<char&,char&>(s[i],t[i]));
                    reversed.insert(std::make_pair<char&,char&>(t[i],s[i]));
                }
            }
        }
        return true;
    }
};
```