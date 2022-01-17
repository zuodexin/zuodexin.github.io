---
title: leetcode1220统计元音字母序列的数目
tags: [leetcode,快速幂,状态机]
---

用f[i][k]表示以第k个字符为结尾的长度为i+1的字符串，可列出动态规划的状态转移方程

```c++
typedef unsigned long long ULL;
class Solution {
    const ULL MOD = 1e9+7;
public:
    int countVowelPermutation(int n) {
        // f[i][0...5] means s[i]== a,e,i,o,u
        // rule a: f[i][0] = f[i-1][1]+f(2)+f(4)
        // f[i][1] = f[i-1][0,2]
        // f[i][2] = f[i-1][1,3]
        // f[i][3] = f[i-1][2]
        // f[i][4] = f[i-1][2,3]
        ULL f[2][5];
        // 注意对双字节数组不能memset非零值
        for(int i=0;i<5;i++){
            f[0][i] = 1;
        }
        ULL cur=0;
        ULL ans=0;
        for(int i=0;i<n-1;i++){
            int next=(cur+1)%2;
            f[next][0] = f[cur][1]+f[cur][2]+f[cur][4];
            f[next][1] = f[cur][0]+f[cur][2];
            f[next][2] = f[cur][1]+f[cur][3];
            f[next][3] = f[cur][2];
            f[next][4] = f[cur][2]+f[cur][3];
            for(int j=0;j<5;j++){
                f[next][j] = f[next][j]%MOD;
            }
            cur = next;
        }
        for(int j=0;j<5;j++){
            ans = (ans+f[cur][j])%MOD;
        }
        return ans;
    }
};
```