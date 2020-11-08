---
title: N皇后
date: 2020-11-08 21:40:38
tags: [leetcode,回溯]
---
阅读全文查看代码
<!--more-->
```c++
class Solution {
   public:
    vector<vector<string>> solveNQueens(int n) {
        vector<vector<string>> res;
        vector<int> queen_col(n, -1);
        helper(n, 0, res, queen_col);
        return res;
    }

    int totalNQueens(int n) {
        vector<vector<string>> res;
        vector<int> queen_col(n, -1);
        helper(n, 0, res, queen_col);
        return res.size();
    }

    void helper(int n, int r, vector<vector<string>> &res,
                vector<int> queen_col) {
        if (n == r) {
            vector<string> solution(n, string(n, '.'));
            for (int i = 0; i < queen_col.size(); i++) {
                solution[i][queen_col[i]] = 'Q';
            }
            res.push_back(solution);
        }
        for (int i = 0; i < n; i++) {
            if (is_valid(r, i, queen_col)) {
                queen_col[r] = i;
                helper(n, r + 1, res, queen_col);
            }
        }
    }

    bool is_valid(int r, int c, vector<int> queen_col) {
        for (int i = 0; i < r; i++) {
            if (c == queen_col[i] || abs(r - i) == abs(c - queen_col[i]))
                return false;
        }
        return true;
    }
};
```