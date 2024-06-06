# BFS of graph


[Problem Link](https://www.geeksforgeeks.org/problems/bfs-traversal-of-graph/1)


## Approach - 1

1. use queue data struture and use visited array to achieve the BFS traversel


```Java

class Solution {
  public:
    // Function to return Breadth First Traversal of given graph.
    vector<int> bfsOfGraph(int V, vector<int> adj[]) {
        // Code here
        
        queue<int> que;
        vector<int> visited(V+1, 0), ans;
        
        que.push(0);
        ans.push_back(0);
        visited[0] = 1;
         
        while(!que.empty()) {
            int node = que.front();
            que.pop();
            
            for(int i=0; i<adj[node].size(); i++) {
                
                if(!visited[adj[node][i]]) {
                    que.push(adj[node][i]);
                    ans.push_back(adj[node][i]);
                    visited[adj[node][i]] = 1;
                }
            }
        }
        return ans;
    }
};

```

## Complexity Analysis:

### Time Complexity: O(N) + O(2E)

### Space Complexity: O(N)