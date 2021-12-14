#### BFS + 状态压缩


```
class Solution {
private:
    static constexpr int  dirs[5][2] ={{0,1},{0,-1},{-1,0},{1,0},{0,0}};

public:

    int encode(vector<vector<int>>& mat) {
        int state=0;
        for(int i=0;i<mat.size();i++){
            for(int j=0;j<mat[i].size();j++){
                state<<=1;
                state += mat[i][j];
            }
        }
        return state;
    }

    int encode_mask(int row,int col,int m,int n){
        int pos = m*n-(row*n+col+1);
        return 1<<pos;
    }

    int convert(int state,int row,int col,int m,int n){
        for(int k=0;k<5;k++){
            int r0=row+dirs[k][0],c0=col+dirs[k][1];
            if (r0>=0 && r0<m && c0>=0 && c0<n){
                int mask = encode_mask(r0,c0,m,n);
                state ^= mask;
            }
        }
        return state;
    }

    void printState(int state){
        std::bitset<4> s(state);
        cout<<s<<endl;
    }

    int minFlips(vector<vector<int>>& mat) {
        int init_state = encode(mat);
        if(init_state==0) return 0;
        unordered_set<int> seen;
        queue<int> q;
        q.push(init_state);
        seen.insert(init_state);
        int m = mat.size();
        int n = mat[0].size();
        int step=0;
        while(!q.empty()){
            ++step;
            int k=q.size();
            for(int _=0;_<k;_++){
                int state0 = q.front();
                q.pop();
                for(int i=0;i<m;i++){
                    for(int j=0;j<n;j++){
                        int state1 = convert(state0,i,j,m,n);
                        if(!seen.count(state1)){
                            seen.insert(state1);
                            q.push(state1);
                        }
                        if(state1==0){
                            return step;
                        }
                    }
                }
            }
        }
        return -1;
    }
};
```