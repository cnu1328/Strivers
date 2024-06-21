# Shortest path in Undirected Graph

[Problem Link](https://www.geeksforgeeks.org/problems/shortest-path-in-undirected-graph-having-unit-distance/1)

## Approach - Use Simple BFS

1. To solve this problem use simple BFS Algorithm
2. Instead of visited array, use distance array
3. If current distance is less than the distance of that node, then change to current distance and push that node to queue.
4. After this, check if any 1e9 value there in distance, if exists replace it with -1 and return the answer

```Java

class Solution {
  public:
    vector<int> shortestPath(vector<vector<int>>& edges, int N,int M, int src){
        // code here
        
        vector<int> adj[N];
        
        for(auto edge : edges) {
            adj[edge[0]].push_back(edge[1]);
            adj[edge[1]].push_back(edge[0]);
        }
        vector<int> dist(N);
        
        for(int i=0; i<N; i++) {
            dist[i] = 1e9;
        }
        dist[src] = 0;
        
        queue<int> que;
        
        que.push(src);
        
        while(!que.empty()) {
            
            int node = que.front();
            que.pop();
            
            for(int child : adj[node]) {
                if(dist[node] + 1 < dist[child]) {
                    dist[child] = dist[node] + 1;
                    que.push(child);
                }
            }
            
        }
        
        vector<int> ans(N, -1);
        
        for(int i=0; i<N; i++) {
            if(dist[i] != 1e9) {
                ans[i] = dist[i];
            }
        }
        
        return ans;
        
    }
};


```

## Complexity Analysis:

### Time Complexity: O(V + 2E)

### Space Complexity: (V)