# Minimum Spanning Tree

[Problem Link](https://www.geeksforgeeks.org/problems/minimum-spanning-tree/1)

## Approach - 1 - Kruskal's Algorithm

<img width="754" alt="image" src="https://github.com/user-attachments/assets/d3bcf4f3-ded7-466f-acdd-fe0ee77f505e">

1. Sort the given edges based on the edge weight
2. Use disjoint set and find the Minimum Spanning Tree

```c++

class DisjointSet {
    vector<int> parent, rank,size;

public:

    DisjointSet(int n) {
        rank.resize(n + 1, 0);
        size.resize(n+1, 1);

        parent.resize(n + 1);

        for(int i=0; i<=n; i++) {
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

        if(rank[pu] < rank[pv]) {
            parent[pu] = pv;
        }
        else if(rank[pu] > rank[pv]) {
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
        } else {
            parent[pv] = pu;
            size[pu] += size[pv];
        }
    }
};


class Solution
{
	public:

    int spanningTree(int V, vector<vector<int>> adj[])
    {
       vector<pair<int, pair<int, int>>> edges;

       for(int i=0; i<V; i++) {
           for(auto it : adj[i]) {
               int child = it[0];
               int weight = it[1];
               int node = i;

               edges.push_back({weight, {node, child}});
           }
       }

       DisjointSet ds(V);

       sort(edges.begin(), edges.end());

       int mst = 0;

       for(auto edge : edges) {
           int wt = edge.first;
           int u = edge.second.first;
           int v = edge.second.second;

           if(ds.findParent(u) != ds.findParent(v)) {
               mst += wt;
               ds.unionByRank(u, v);
           }
       }

       return mst;
    }
};

```

## Complexitiy Analysis:

### Time Complexity : O(N+E) + O(E logE) + O(E\*4α\*2)

### Space Compleixty : O(N) + O(N) + O(E)
