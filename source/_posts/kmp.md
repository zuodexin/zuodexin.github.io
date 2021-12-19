
#### KMP算法

关键是算next数组

后续计算可视为对 needle + "#"(不存在的字符) + haystack 再算一次next数组

需要背下来。。。



```
class Solution {
public:
    int strStr(string haystack, string needle) {
        int m=haystack.size(),n=needle.size();
        if(n==0) return 0;
        if(n>m) return -1;
        vector<int> next(n,0);
        for(int i=1,j=0;i<n;i++){
            while(j>0 && needle[i]!=needle[j])
                j = next[j-1];
            if(needle[i]==needle[j])
                j++;
            next[i] = j;
        }
        for(int i=0,j=0;i<m;i++){
            while(j>0 && haystack[i]!=needle[j])
                j = next[j-1];
            if(haystack[i]==needle[j])
                j++;
            if(j==n) return i-n+1;
        }
        return -1;
    }
};
```