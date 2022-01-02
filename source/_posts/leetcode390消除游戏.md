---
title: leetcode390消除游戏
date: 2020-11-22 10:41:02
tags: [leetcode,找规律]
---

找规律问题

约瑟夫环（约瑟夫问题）是一个数学的应用问题：已知 n 个人（以编号1，2，3…n分别表示）围坐在一张圆桌周围。从编号为 k 的人开始报数，数到 m 的那个人出圈；他的下一个人又从 1 开始报数，数到 m 的那个人又出圈；依此规律重复下去，直到剩余最后一个胜利者。

约瑟夫环中，每当有一个人出圈，出圈的人的下一个人成为新的环的头，相当于把数组向前移动 m 位。若已知 n-1 个人时，胜利者的下标位置位 f(n−1,m) ，则 n 个人的时候，就是往后移动 m 位，(因为有可能数组越界，超过的部分会被接到头上，所以还要模 n )，根据此推导过程得到的计算公式为：
```
f(n,m) = (f(n−1,m) + m) % n
```
其中，f(n,m) 表示 n 个人进行报数时，每报到 m 时杀掉那个人，最终的编号，f(n−1,m) 表示，n-1 个人报数，每报到 m 时杀掉那个人，最终胜利者的编号。有了递推公式后即可使用递归的方式实现。

```c++
class Solution {
public:
    int lastRemaining(int n) {
        return func(n,false)+1;
    }

    int func(int n,bool reverse){
        int ans = 0;
        if(n!=1){
            ans = 2*func(n/2,!reverse)+int((!reverse)||(n%2));
        }
        //printf("func(%d,%d)=%d\n",n,reverse,ans);
        return ans;
    }
};
```