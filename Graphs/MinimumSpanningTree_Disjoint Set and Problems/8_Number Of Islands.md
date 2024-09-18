# Number Of Islands

[Problem Link](https://www.geeksforgeeks.org/problems/number-of-islands/1)

## Approach - 1 - DSU

1. Repersent every cell as a node
2. For every operations (row, col), check if its adjacent indices have an island (1), then union operation node to the island node
3. For every operation find the number of components and mark ans[i] = components
4. return the answer array

<img width="735" alt="image" src="https://github.com/user-attachments/assets/4aa2173e-9524-421d-8201-0d2e2dca2a96">

```c++

class DisjointSet {

public:
    vector<int> parent, rank, size;
    DisjointSet(int v) {
        parent.resize(v);
        rank.resize(v, 0);
        size.resize(v, 1);

        for(int i=0; i<v; i++) {
            parent[i] = i;
        }
    }

    int findParent(int node) {
        if(node == parent[node]) return node;

        return parent[node] = findParent(parent[node]);
    }

    void unionByRank(int u, int v) {
        int pu = findParent(u);
        int pv = findParent(v);

        if(pu == pv) return;

        if(rank[pu] > rank[pv]) {
            parent[pu] = pv;
        }

        else if(rank[pu] < rank[pv]) {
            parent[pv] = pu;
        }

        else {
            parent[pv] = pu;
            rank[pv] ++;
        }
    }

    void unionBySize(int u, int v) {
        int pu = findParent(u);
        int pv = findParent(v);

        if(pu == pv) return;

        if(size[pu] < size[pv]) {
            parent[pu] = pv;
            size[pv] += size[pu];
        }

        else {
            parent[pv] = pu;
            size[pu] += size[pv];
        }
    }
};

class Solution {
  public:
    vector<int> numOfIslands(int n, int m, vector<vector<int>> &oper) {

        DisjointSet ds(n * m);

        vector<vector<int>> island(n, vector<int> (m, 0));

        int k = oper.size();

        vector<int> ans(k);

        int dir[] = {-1, 0, 1, 0, -1};

        for(int i=0; i<k; i++) {
            int row = oper[i][0];
            int col = oper[i][1];

            int node = row * m + col;

            for(int i=0; i<4; i++) {
                int newr = row + dir[i];
                int newc = col + dir[i + 1];

                if(newr < 0 || newr >= n || newc < 0 || newc >= m) continue;

                if(island[newr][newc] == 1) {
                    int node1 = newr * m + newc;

                    ds.unionBySize(node, node1);
                }
            }

            island[row][col] = 1;

            int components = 0;

            // cout<<i<<endl;

            for(row = 0; row < n; row ++) {

                // node = -1;

                for(col = 0; col < m; col ++) {

                    // cout<<island[row][col]<<" ";
                    if(island[row][col] == 1) {

                        node = row * m + col;

                        if(ds.findParent(node) == node) {
                            components ++;
                        }
                    }
                }

                // cout<<"  "<<node<<endl;
            }

            ans[i] = components;
        }

        return ans;
    }
};

```

## Complexitiy Analysis:

### Time Complexity : O(k \* N \* M \* 4 \* alpha)

### Space Compleixty : O(M\*N)


```cpp

class DisjointSet {

public:
vector<int> parent, size;

    DisjointSet(int n) {
        parent.resize(n + 1);
        size.resize(n + 1, 1);

        for(int i=0; i<=n; i++) {
            parent[i] = i;
        }
    }

    int findParent(int node) {
        if(node == parent[node]) return node;

        return parent[node] = findParent(parent[node]);
    }

    void unionBySize(int u, int v) {
        int pu = findParent(u);
        int pv = findParent(v);

        if(pu == pv) return;

        if(size[pu] < size[pv]) {
            parent[pu] = pv;
            size[pv] += size[pu];
        }

        else {
            parent[pv] = pu;
            size[pu] += pv;
        }
    }

};

class Solution {
public:
int countSubIslands(vector<vector<int>>& grid1, vector<vector<int>>& grid2) {

        int n = grid1.size();
        int m = grid1[0].size();

        DisjointSet ds(n * m);

        int dir[] = {-1, 0, 1, 0, -1};

        for(int i=0; i<n; i++) {
            for(int j=0; j<m; j++) {

                if(grid2[i][j] && grid1[i][j]) {

                    for(int k=0; k<4; k++) {

                        int newx = i + dir[k];
                        int newy = j + dir[k + 1];

                        if(newx < 0 || newy < 0 || newx >= n || newy >= m) continue;

                        if(grid2[newx][newy] && grid1[newx][newy]) {
                            int node1 = m * i + j;
                            int node2 = m * newx + newy;

                            ds.unionBySize(node1, node2);
                        }

                    }
                }
            }
        }

        int ans = 0;

        for(int i=0; i<n; i++) {
            for(int j=0; j<m; j++) {

                int node = m * i + j;

                if(grid1[i][j] && grid2[i][j]) {

                    if(ds.findParent(node) == node) {
                        cout<<i<<" "<<j<<endl;
                        ans ++;
                    }
                }
            }
        }

        for(int i=0; i<ds.parent.size(); i++) {
            cout<<ds.parent[i]<<" ";
        }

        return ans;



    }

};

```
