---
title: leetcode简单题汇总
tags: [leetcode,双指针,找规律]
---

<!--more-->

1716. 计算力扣银行的钱

找规律，应用等差数列求和公式

```c++
class Solution {
public:
    int totalMoney(int n) {
        int week = (n-1)/7;
        int day = (n-1)%7;
        /*
            1,2,3,4,5,6,7
            2,3,4,5,6,7,8 = sum(week 1)+7
            3,4,5,6,7,8,9 = sum(week 1)+7*2
        */
        int before = week*(1+7)*7/2 + 7*(week-1)*week/2;
        int sum = before;
        for(int i=0;i<=day;i++){
            int base = week+1;
            sum += base + i;
        }
        return sum;
    }
};
```


167. 两数之和 II - 输入有序数组

双指针，初始化时，l只能往右，r只能往左

P(l,r) 表示在$[l,r]上搜索问题的解，P(l,r) 可以分解为 P(l+1,r)，P(l,r-1)

当$numbers[l]+numbers[r] < target$，l+1或者r+1都有可能使和增大，但r+1已经搜索过了，所以只能l+1


```c++
class Solution {
public:
    vector<int> twoSum(vector<int>& numbers, int target) {
        int n = numbers.size();
        int l=0,r=n-1;
        vector<int> ans(2,-1);
        while(l<r){
            if(numbers[l]+numbers[r]==target){
                ans[0] = l+1;
                ans[1] = r+1;
                return ans;
            }
            if(numbers[l]+numbers[r]>target){
                r--;
            }else{
                l++;
            }
        }
        return ans;
    }
};
```

557. 反转字符串中的单词 III

```c++
class Solution {
public:
    string reverseWords(string s) {
        int start=0,end,l,r,n=s.size();
        string ans(s);
        while(start<n){
            while(start<n && ans[start]==' ') start++;
            end = start;
            while(end<n && ans[end]!=' ') end++;
            l = start;
            r = end-1;
            while(l<r){
                swap(ans[l],ans[r]);
                l++;
                r--;
            }
            start = end;
        }
        return ans;
    }
};
```
876. 链表的中间节点

双指针，快的指针走两步，慢的指针走一步，直到快的指针指向链表结尾

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* middleNode(ListNode* head) {
        ListNode dummy= ListNode(0,head);
        ListNode* l=&dummy,*r=&dummy;
        while(l!=nullptr && r!=nullptr){
            l=l->next;
            for(int i=0;i<2;i++){
                if(r) r = r->next;
            }
        }
        return l;
    }
};
```

leetcode733 图片上色

注意要对bfs路径上的每个节点做一些操作最好在取出队列开头元素之后立刻进行，如果在入队之前做会漏掉初始点

注意visited被设置为1的时机，不能忘记对visited做初始化

```c++
class Solution {
    const int dirs[4][2] = {{1,0},{0,1},{-1,0},{0,-1}};
public:
    vector<vector<int>> floodFill(vector<vector<int>>& image, int sr, int sc, int newColor) {
        queue<pair<int,int>> q;
        q.push({sr,sc});
        int m= image.size(),n=image[0].size();
        int srcColor = image[sr][sc];
        vector<vector<int>> ans(m,vector<int>(n,0));
        vector<vector<int>> visited(m,vector<int>(n,0));
        for(int i=0;i<m;i++)
            for(int j=0;j<n;j++)
                ans[i][j] = image[i][j];
        visited[sr][sc] = 1;

        while(!q.empty()){
            pair<int,int> pos = q.front();
            q.pop();
            //cout<<"("<<pos.first<<","<<pos.second<<"):"<<srcColor<<endl;
            if(image[pos.first][pos.second]==srcColor) ans[pos.first][pos.second]=newColor;
            for(int i=0;i<4;i++){
                pair<int,int> np;
                np.first =pos.first+dirs[i][0];
                np.second =pos.second+dirs[i][1];
                if(np.first>=0 && np.first<m && np.second>=0 && np.second<n && !visited[np.first][np.second]&& image[np.first][np.second]==srcColor){
                    q.push(np);
                    visited[np.first][np.second]=1;
                }
            }
        }
        return ans;
    }
};
```

岛屿最大面积

grid本身充当visited，注意初始化


```c++
struct Point{
    int x,y;
    Point(int x,int y):x(x),y(y){};
};

class Solution {
    const int dirs[4][2]{{0,1},{1,0},{-1,0},{0,-1}};
public:
    int maxAreaOfIsland(vector<vector<int>>& grid) {
        int m=grid.size(),n=grid[0].size();
        // vector<vector<int>> visited(m,vector<int>(n,0));
        int ans=0;
        for(int i=0;i<m;i++){
            for(int j=0;j<n;j++){
                if(grid[i][j]){
                    ans = max(ans,bfs(grid,i,j));
                    //cout<<ans<<endl;
                }
            }
        }
        return ans;
    }

    int bfs(vector<vector<int>>& grid,int r,int c){
        int m=grid.size(),n=grid[0].size();
        queue<Point> q;
        q.push(Point(r,c));
        grid[r][c] = 0;
        int area=0;
        while(!q.empty()){
            Point p = q.front();
            q.pop();
            area++;
            //cout<<p.x<<","<<p.y<<endl;
            for(int i=0;i<4;i++){
                Point np(p.x+dirs[i][0],p.y+dirs[i][1]);
                if(np.x>=0 && np.x<m && np.y>=0 && np.y<n && grid[np.x][np.y]!=0){
                    grid[np.x][np.y]=0;
                    q.push(np);
                }
            }
        }
        return area;
    }

};
```

leetcode617. 合并二叉树

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    TreeNode* mergeTrees(TreeNode* root1, TreeNode* root2) {
        if(root1==nullptr || root2==nullptr) return root1==nullptr?root2:root1;
        TreeNode *root = new TreeNode();
        root->val = root1->val+root2->val;
        root->left = mergeTrees(root1->left,root2->left);
        root->right = mergeTrees(root1->right,root2->right);
        return root;
    }
};
```

leetcode219. 存在重复元素

哈希表或者滑动窗口

```c++
class Solution {
public:
    bool containsNearbyDuplicate(vector<int>& nums, int k) {
        map<int,int> loc;
        for(int i=0;i<nums.size();i++){
            if(loc.count(nums[i])){
                int last = loc[nums[i]];
                if(i-last<=k){
                    return true;
                }
            }
            loc[nums[i]]=i;
        }
        return false;
    }
};
```