---
title: 和为K的最短子数组
date: 2020-11-08 21:44:04
tags: [leetcode,数组]
---
阅读全文查看代码
<!--more-->
```c++
class Solution {
   public:
    int shortestSubarray(vector<int> arr, int k) {
        int ans = INT_MAX;
        int sum = 0;
        int n = arr.size();
        priority_queue<pair<int, int>, vector<pair<int, int>>,
                       greater<pair<int, int>>>
            pq;
        for (int i = 0; i < n; i++) {
            sum += arr[i];
            if (sum >= k) ans = min(ans, i + 1);
            while (!pq.empty() && sum - pq.top().first >= k) {
                ans = min(ans, i - pq.top().second);
                pq.pop();
            }
            pq.push(make_pair(sum, i));
        }
        return (ans == INT_MAX) ? -1 : ans;
    }
};
```