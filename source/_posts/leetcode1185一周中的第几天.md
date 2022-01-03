
---
title: leetcode1185 一周中的第几天
tags: [leetcode,仿真]
---
注意闰年的判断条件

```c++
class Solution {
public:
    string dayOfTheWeek(int day, int month, int year) {
        int dayCnt[]{
            31,28,31,30,31,30,31,31,30,31,30,31
        };
        string dayNames[]{"Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"};
        unsigned int ans = 4;
        for(int i=1971;i<year;i++){
            bool isLeap = i%4==0?(i%100==0?i%400==0:true):false;
            ans += 365+int(isLeap);
            //if(i==2000) cout<<isLeap<<endl;
        }
        bool curIsLeap = year%4==0?(year%100==0?year%400==0:true):false;
        // cout<<curIsLeap<<endl;
        for(int i=0;i+1<month;i++){
            ans += dayCnt[i]+int(i==1 && curIsLeap);
        }
        ans += day;
        return dayNames[ans%7];
    }
};
```