# DFS of Graph

[Problem Link](https://www.geeksforgeeks.org/problems/depth-first-traversal-for-a-graph/1)

## Approach
1. use recurrsion to visit the depth nodes first


```Java

class Solution {
  public:
    
    void dfs(int node, vector<int> adj[], vector<int> &visited, vector<int> &ans) {
        visited[node] = 1;
        ans.push_back(node);
        
        for(int it : adj[node]) {
            
            if(!visited[it])
                dfs(it, adj, visited, ans);
        }
    }
  
    // Function to return a list containing the DFS traversal of the graph.
    vector<int> dfsOfGraph(int V, vector<int> adj[]) {
        // Code here
        
        vector<int> ans, visited(V+1);
        dfs(0, adj, visited, ans);
        return ans;
    }
};

```

## Complexity Analysis:

### Time Complexity: O(N)(for every node) + O(2E)(at every node, summation of degrees)

### Space Complexity: O(N)(for answer) + O(N)(for visited) + O(N)(Stack Space) => O(N) 