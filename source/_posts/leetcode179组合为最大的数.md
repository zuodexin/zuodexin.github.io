---
title: leetcode179组合为最大的数
date: 2020-11-09 23:48:16
tags: [leetcode]
---

不知道为什么我的答案出现越界错误，改成简单的答案就不会出错了

权当掌握lambda表达式和string的比较罢了，有空再看


<!--more-->

```c++
string int2string(int i){
    stringstream ss;
    string s;
    ss<<i;
    ss>>s;
    return s;
}
string combine(int a,int b){
    string sa,sb;
    sa = int2string(a);
    sb = int2string(b);
    return sa+sb;
};
bool str_le(string a,string b){
    int i=0,j=0;
    while(a[i]=='0' && i<a.size()) i++;
    while(b[j]=='0' && j<b.size()) j++;
    if(a.size()-i!=b.size()-j) return a.size()-i<b.size()-j;
    else{
        while(i<a.size() && j<b.size() ){
            if(a[i]==b[j]){
                i++;
                j++;
            }
            else return a[i]<b[j];
        }
        return true;
    }
};
bool less_than(int a,int b){
    // return true;
    return str_le(combine(a,b),combine(b,a));
};

class Solution {
public:
    string largestNumber(vector<int>& nums) {
        std::sort(nums.begin(),nums.end(),[](int a,int b){
            return (to_string(a)+to_string(b))<(to_string(b)+to_string(a));
        });
        string s;
        for(int i=nums.size()-1;i>=0;i--){
            cout<<i<<endl;
            if(s.size()>0||nums[i]!=0)
                s += int2string(nums[i]);
        }
        if(s.size()==0) s="0";
        return s;
    }
};
```


```c++
bool str_le(const string& a,const string& b){
    int i=0,j=0;
    while(i<a.size() && a[i]=='0') i++;
    while(j<b.size() && b[j]=='0') j++;
    if(a.size()-i!=b.size()-j) return a.size()-i<b.size()-j;
    else{
        while(i<a.size() && j<b.size() ){
            if(a[i]==b[j]){
                i++;
                j++;
            }
            else return a[i]<b[j];
        }
        return true;
    }
};

class Solution {
public:
    string largestNumber(vector<int>& nums) {
        struct {
            bool operator()(int& a,int& b) const{
                const string& ab = to_string(a)+to_string(b);
                const string& ba = to_string(b)+to_string(a);
                return str_le(ab,ba);
            }; 
        } obj;
        std::sort(nums.begin(),nums.end(),obj);
        string s;
        for(int i=nums.size()-1;i>=0;i--){
            if(s.size()>0||nums[i]!=0)
                s += to_string(nums[i]);
        }
        if(s.size()==0) s="0";
        return s;
    }
};
```