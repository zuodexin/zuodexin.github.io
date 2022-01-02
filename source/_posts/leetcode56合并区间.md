---
title: leetcode56合并区间
date: 2020-11-22 10:41:02
tags: [leetcode,优先队列,双指针,STL]
---

如果需要this是const，要在函数的花括号前面加const关键字

优先队列返回的都是const对象，和其他STL数据结构还不一样


```c++
struct Interval{
    int start;
    int end;
    Interval(int start,int end):start(start),end(end){

    };
    bool operator < (const Interval& b) const{
        return !(start<b.start);
    };
};


class Solution {
public:
    vector<vector<int>> merge(vector<vector<int>>& intervals) {
        vector<vector<int>> ans;
        priority_queue<Interval> queue;
        for(int i=0;i<intervals.size();i++){
            Interval interval(intervals[i][0],intervals[i][1]);
            queue.push(interval);
        }
        while(!queue.empty()){
            const Interval cur = queue.top();
            queue.pop();
            if(queue.empty()){
                vector<int> v{cur.start,cur.end};
                ans.push_back(v);
                break;
            }
            const Interval top = queue.top();
            queue.pop();
            if(cur.end>=top.start){
                const Interval merged(cur.start,max(top.end,cur.end));
                queue.push(merged);
            }else{
                vector<int> v{cur.start,cur.end};
                ans.push_back(v);
                queue.push(top);
            }
        }
        return ans;
    }

};
```