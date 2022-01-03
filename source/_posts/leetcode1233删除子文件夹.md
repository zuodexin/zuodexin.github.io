
---
title: leetcode1233 删除子文件夹
tags: [leetcode,字典树]
---



```c++

#define MAX_N 500000

struct Trie{
    int nex[MAX_N][27]={0},cnt=0;
    int exist[MAX_N]={0};

    void insert(const string& s){
        int l = s.size();
        int p = 0;
        for(int i=0;i<l;i++){
            int c= s[i]=='/'?26:s[i]-'a';
            if(!nex[p][c]) nex[p][c] = ++cnt;
            assert(cnt<MAX_N);
            p = nex[p][c];
        }
        exist[p] = 1;
    };

    bool find(const string& s){
        int p=0;
        for(int i=0;i<s.size();i++){
            int c = s[i]=='/'?26:s[i]-'a';
            p = nex[p][c];
            if(!exist[p]) return false;
        }
        return false;
    };
};

struct QItem{
    int id;
    string s;
    int child;
    QItem(int id,string s,int c):id(id),s(s),child(c){};
};

ostream& operator << (ostream& out,const QItem& q){
    out<<"id:"<<q.id<<"s:"<<q.s;
    return out;
};


class Solution {
public:
    vector<string> removeSubfolders(vector<string>& folder) {
        Trie trie;
        for(string s:folder){
            trie.insert(s);
        }
        queue<QItem> q;
        q.push(QItem(0,"",27));
        vector<string> ans;
        while(!q.empty()){
            QItem p=q.front();
            q.pop();
            for(int i=0;i<p.child;i++){
                int c = trie.nex[p.id][i];
                if(!c) continue;
                stringstream ss;
                ss<<p.s<<char(i==26?'/':'a'+i);
                string curs=ss.str();
                //cout<<p<<curs<<"i:"<<i<<endl;
                if(i<26 && trie.exist[c]){ 
                    ans.push_back(curs);
                    QItem item(c,curs,26);
                    q.push(item);
                }else{
                    QItem item(c,curs,27);
                    q.push(item);
                }
            }
        }
        return ans;
    }
};

```