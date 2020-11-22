---
title: leetcode777交换LR字符串
date: 2020-11-21 23:28:16
tags: [leetcode]
---

看懂题目之后很好理解，变换中L只能往左移动，R只能往右移动，因此用双指针就可以了。

<!--more-->

```c++
class Solution {
public:
    bool canTransform(string start, string end) {
        if(start.size()!=end.size()) return false;
        int i=0,j=0;
        while(true){
            // cout<<"i: "<<i<<" j:"<<j<<endl;
            while(i<start.size()&&start[i]=='X') i++;
            while(j<end.size()&&end[j]=='X') j++;
            if(i==start.size()||j==end.size()) break;
            if(start[i]!=end[j]) return false;
            else if(start[i]=='R'){
                if(i<=j){ 
                    i++;
                    j++;
                }else return false;
            }else if(start[i]=='L'){
                if(i>=j){
                   i++;
                   j++;
                }else return false;   
            }
        }
        if(i==start.size()&&j==end.size()) return true;
        else return false;
    }
};
```