---
title: leetcode334递增的三元子序列
tags: [leetcode,贪心，单调栈]
---


```c++
class Solution {
public:
    bool increasingTriplet(vector<int>& nums) {
        int n = nums.size();
        if(n<3) return false;
        stack<int> st;
        st.push(nums[0]);
        vector<int> cum(n,0);
        cum[n-1] = nums[n-1];
        for(int i=n-2;i>=0;i--){
            cum[i] = max(nums[i],cum[i+1]);
        }
        for(int i=1;i<n;i++){
            if(st.size()==0 || nums[i]>st.top()){
                st.push(nums[i]);
                if(st.size()==3) return true;
            }else{
                if(st.size()==2 && cum[i]>st.top()) return true;
                while(st.size()>0 && nums[i]<=st.top()){
                    st.pop();
                }
                st.push(nums[i]);
            }
        }
        return false;
    }
};
```