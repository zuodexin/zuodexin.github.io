---
title: leetcode89格雷编码
tags: [leetcode,位运算,DFS]
mathjax: true
---

用dfs做复杂度是$O((n-1)!)$,在超时的边缘徘徊
```c++
class Solution {
public:
    vector<int> grayCode(int n) {
        vector<int> seq{0};
        set<int> seen{0};
        dfs(n,1,seq,seen);
        return seq;
    }
    int bit_count(int x){
        return x==0?0:(x&1)+bit_count(x>>1);
    }

    bool dfs(int n,int idx, vector<int>& seq,set<int>& seen){
        if(idx>=(1<<n)){
            return true;
        }
        for(int i=0;i<n;i++){
            int last = seq[idx-1];
            int logit = 1<<i;
            int cur = last ^ logit;
            if(!seen.count(cur)){
                if(idx==(1<<n)-1){
                    if(bit_count(cur^seq[0])!=1) continue;
                }
                seen.insert(cur);
                seq.push_back(cur);
                if(!dfs(n,idx+1,seq,seen)){
                    seen.erase(cur);
                    seq.pop_back();
                }else{
                    return true;
                }
            }
        }
        return false;
    }
};
```

如果找到格雷码的规律，复杂度可以将到O(2^n)
将$G_{n-1}$翻转得到$R{n-1}$,在 $concat(G_{n-1},R_{n-1})$的高位分别拼接0和1得到$G_{n}$

遇到找规律的题目，要想代码写对，最好列一个表格出来，想明白迭代的次数

```c++
0   1   2   3
0   0   0|0 0|00
    1   0|1 0|01
        1|1 0|11
        1|0 0|10
            1|10
            1|11
            1|01
            1|00
 ```

```c++
class Solution {
public:
    vector<int> grayCode(int n) {
        vector<int> seq{0};
        for(int i=0;i<n;i++){
            for(int j=0;j<1<<i;j++){
                seq.push_back(seq[(1<<i)-1-j]|(1<<i));
            }
        }
        return seq;
    }
};
```