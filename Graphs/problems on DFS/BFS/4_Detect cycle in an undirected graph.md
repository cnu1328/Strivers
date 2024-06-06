# Detect cycle in an undirected graph

[Problem Link](https://www.geeksforgeeks.org/problems/detect-cycle-in-an-undirected-graph/1)

## Approach - Using BFS

1. As we know BFS is a traverse technique, that traverse level wise
2. If we get a node and the is visited, then the graph contain cycle if the node is not its parent.
3. return true or false


```Java

class Solution {
    
  private: 
  
    bool bfs(int src, vector<int> adj[], vector<int> &visited) {
        
        visited[src] = 1;
        
        queue<pair<int,int>> que;
        que.push({src, -1});
        
        while(!que.empty()) {
            int child = que.front().first;
            int parent = que.front().second;
            
            que.pop();
            
            for(int node : adj[child]) {
                
                if(!visited[node]) {
                    que.push({node, child});
                    visited[node] = 1;
                }
                
                else if(parent != node) return true;
                
                
            }
        }
        
        return false;
        
    }
    
  public:
    // Function to detect cycle in an undirected graph.
    bool isCycle(int V, vector<int> adj[]) {
        
        vector<int> visited(V);
        
        for(int i=0; i<V; i++) {
            if(!visited[i] && bfs(i, adj, visited)) return true; 
        }
        

       
        return false;
    }
};


```


## Complexity Analysis:

### Time Complexity: O(V + 2E) + O(N)

### Space Complexity: O(N)



## Approach - Using DFS

```Java

class Solution {
    
  private:
    
    bool dfs(int src, int parent,vector<int> adj[],vector<int>  &visited) {
        visited[src] = 1;
        
        for(int node : adj[src]) {
            if(!visited[node]) {
                if(dfs(node, src, adj, visited)) return true;
            }
            
            else if(parent != node) return true;
        }
        
        return false;
    } 
    
  public:
    // Function to detect cycle in an undirected graph.
    bool isCycle(int V, vector<int> adj[]) {
        // Code here
        
        vector<int> visited(V);
        // To check for every connected component
        for(int i=0; i<V; i++) {
            if(!visited[i] && dfs(i, -1, adj, visited)) return true;
        }
        return false;
    }
};

```

## Complexity Analysis:

### Time Complexity: O(V + 2E) + O(N)

### Space Complexity: O(N)