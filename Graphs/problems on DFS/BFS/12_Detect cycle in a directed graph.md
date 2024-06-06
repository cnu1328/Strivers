# Detect cycle in a directed graph

[Problem Link](https://www.geeksforgeeks.org/problems/detect-cycle-in-a-directed-graph/1)

## Approach - Using DFS

1. The algorithm we used for detecting a cycle in undirectd graph will not work here
2. The cycle can be detected on the same path the node has to be visited again

```Java

class Solution {
  private: 
  
    bool dfs(int node, int visited[], int path[], vector<int> adj[]) {
        
        visited[node] = 1;
        path[node] = 1;
        
        for(int child : adj[node]) {
            if(!visited[child]) {
                if(dfs(child, visited, path, adj) == true)
                 return true;
            } 
            
            else if(path[child]) return true;
        }
        
        path[node] = 0;
        
        return false;
    }
  public:
    // Function to detect cycle in a directed graph.
    bool isCyclic(int V, vector<int> adj[]) {
        // code here
        int visited[V] = {0};
        int path[V] = {0};
        
        for(int i=0; i<V; i++) {
            if(!visited[i] && dfs(i, visited, path, adj) == true) 
                return true;
        }
        
        return false;
    }
};

```

## Complexity Analysis:

### Time Complexity: (V + E)

### Space Complexity: (V)

