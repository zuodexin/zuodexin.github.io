---
title: leetcode71简化路径
tags: [leetcode,字符串]
---

用vector存储路径上的每个元素，用`/`分割字符串，遇到`.`不处理，遇到`..`删除vector最后一个元素，注意连续的`/`处理。


```c++
class Solution {
public:
    string simplifyPath(string path) {
        vector<string> mem;
        int start=0;
        while(start<path.size() && path[start]=='/'){
                start++;
        }
        while(start<path.size()){
            int i=start;
            while(i<path.size() && path[i]!='/'){
                i++;
            }
            string s = path.substr(start,i-start);
            if(s=="."){

            }else if (s==".."){
                if(mem.size()>0) mem.pop_back();
            }else{
                mem.push_back(s);
            }
            start = i;
            while(start<path.size() && path[start]=='/'){
                start++;
            }
        }
        string ans = "/";
        for(int i=0;i<mem.size();i++){
            ans = i==0?ans+mem[i]:ans+"/"+mem[i];
        }
        return ans;
    }
};
```