---
title: leetcode306,累加数
tags: [leetcode,dfs]
---

遍历前两个数的组合，那么剩余的字符串如果是累加数，那么是可以确定的

注意题目要求数字不能以0开头

```c++
class Solution {
public:
    bool isAdditiveNumber(string num) {
        if(num.size()<3) return false;
        for(int i=1;i<num.size()/2+1;i++){
            for(int j=1;i+j<num.size();j++){
                string num1 = num.substr(0,i);
                string num2 = num.substr(i,j);
                string remain = num.substr(i+j,num.size()-i-j);
                if(dfs(num1,num2,remain)) return true;
            }
        }
        return false;
    }

    bool dfs(const string& num1,const string& num2,const string& remain){
        if(remain.size()==0) return true;
        if(num1.size()>1 && num1[0]=='0') return false;
        if(num2.size()>1 && num2[0]=='0') return false;
        string sum = add(num1,num2);
        //cout<<"num1:"<<num1<<",num2:"<<num2<<",sum:"<<sum<<",remain:"<<remain<<endl;
        const char* p = strstr(remain.c_str(),sum.c_str());
        if(p && strlen(p)==remain.size()){
            //cout<<"sum:"<<sum<<endl;
            return dfs(num2,sum,remain.substr(sum.size(),remain.size()-sum.size()));
        }
        return false;
    }

    string add(const string& a,const string& b){
        const string*  large = &a, *small = &b ;
        if(a.size()<b.size()){
            large = &b;
            small = &a;
        }
        string ans = "0"+*large;
        int i=large->size()-1,j = small->size()-1;
        int c=0;
        while(c!=0||i>=0){
            if(i>=0&&j>=0){
                int s = c+(*large)[i]-'0'+(*small)[j]-'0';
                c = s/10;
                ans[i+1] = '0'+s%10;
                i--;
                j--;
            }else if(i>=0){
                int s = c+(*large)[i]-'0';
                c = s/10;
                ans[i+1] = '0'+s%10;
                i--;
            }else{
                ans[0] = c+'0';
                c = 0;
            }
            //cout<<"i:"<<i<<",j:"<<j<<",c:"<<c<<endl;
        }
        if(ans[0]=='0'){
            ans = ans.substr(1,ans.size()-1);
        }
        return ans;
    }
};
```