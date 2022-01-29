---
title: leetcode539最小时间差
tags: [leetcode,排序,数学]
---


```c++
struct Time {
    int hour,minute;
    Time(){};
    Time(int hour,int minute):hour(hour),minute(minute){};
    bool operator < (const Time & b) const{
        if(hour==b.hour){
            return minute<b.minute;
        }
        return hour<b.hour;
    };
    int operator-(const Time& b) const{
        Time small=*this,big=b;
        if(big<small){
            swap(small,big);
        }
        int d1 = big.hour*60+big.minute-(small.hour*60+small.minute);
        int d2 = 24*60-d1;
        return min(d1,d2);
    };
};

class Solution {
public:
    int findMinDifference(vector<string>& timePoints) {
        if(timePoints.size()>24*60) return 0;
        vector<Time> arr;
        for(int i=0;i<timePoints.size();i++){
            Time t;
            t.hour = atoi(timePoints[i].substr(0,2).c_str());
            t.minute = atoi(timePoints[i].substr(3,2).c_str());
            //cout<<t.hour<<","<<t.minute<<endl;
            arr.push_back(t);
        }
        sort(arr.begin(),arr.end());
        int ans=24*60;
        for(int i=1;i<=arr.size();i++){
            ans = min(ans,arr[i%arr.size()]-arr[i-1]);
        }
        return ans;
    }
};
```