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

## Approach - Using DFS - Toposort - Khan's Algorithm

1. Implement Khan's Algorithm, which specifies that, take indegree count for all nodes
2. Take a queue, and push nodes to queue, if its indegree is zero
3. Apply BFS on it
4. After BFS, if the inDegree frequencies are greater than zero then return true(Cycle is detected)
5. other wise cycle is not there
6. Insted, you also verify with the help of count of toposort count
7. If toposort count is equal to V then return flase
8. Other wise return true

```Java

class Solution {
    // Function to detect cycle in a directed graph.
    public boolean isCyclic(int V, ArrayList<ArrayList<Integer>> adj) {
        // code here
        
        int inDegree[] = new int[V];
        
        for(int i=0; i<V; i++) {
            for(Integer node : adj.get(i)) {
                inDegree[node]++;
            }
        }
        
        Queue<Integer> queue = new LinkedList<>();
        
        for(int i=0; i<V; i++) {
            if(inDegree[i] == 0) queue.add(i);
        }
        
        int toposort = 0;
        
        while(!queue.isEmpty()) {
            int node = queue.poll();
            toposort++;
            
            for(Integer child : adj.get(node)) {
                inDegree[child]--;
                
                if(inDegree[child] == 0) {
                    queue.add(child);
                }
            }
        }
        
        if(toposort == V) return false;
        
        
        return true;
    }
}


```

## Complexity Analysis:

### Time Complexity: (V + E)

### Space Complexity: (V)
