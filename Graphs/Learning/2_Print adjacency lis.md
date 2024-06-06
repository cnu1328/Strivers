# Print adjacency list

[Problem Link](https://www.geeksforgeeks.org/problems/print-adjacency-list-1587115620/1)


## Approach

```Java

class Solution {
  public:
    // Function to return the adjacency list for each vertex.
    vector<vector<int>> printGraph(int V, vector<pair<int,int>>edges) {
        // Code here
        
        vector<vector<int>> adj(V + 1);
        
        int n = edges.size();
        
        for(int i=0; i<n; i++) {
            int u = edges[i].first;
            int v= edges[i].second;
            
            adj[v].push_back(u);
            adj[u].push_back(v);
        }
        
        return adj;
    }
};

```

```Java


//User function Template for Java
class Solution {
    public List<List<Integer>> printGraph(int V, int edges[][]) {
        List<List<Integer>> adj = new ArrayList<>();
        
        int n = edges.length;
        
        for(int i=0; i<V; i++) {
            adj.add(new ArrayList<>());
        }
        
        for(int i=0; i<n; i++) {
            int u = edges[i][0];
            int v = edges[i][1];
            
            adj.get(u).add(v);
            adj.get(v).add(u);
        }
        
        return adj;
        
    }
}


```

## Complexity Analysis:

### Time Complexity: O(N)

### Space Complexity: O(E)