# Shortest path in Directed Acyclic Graph


[Problem Link](https://www.geeksforgeeks.org/problems/shortest-path-in-undirected-graph/1)


## Approach - Using Toposort and relaxing the edges

1. First find the toposort for the given graph( using BFS or DFS)
2. Then, take an element from stack and relax the edges
3. Mean while have distance array, which always store the minimum distance

```Java


class Pair {
    int node;
    int dist;
    
    Pair(int node, int dist) {
        this.node = node;
        this.dist = dist;
    }
}

//User function Template for Java
class Solution {
    
    void dfs(int node, int visited[], Stack<Integer> st, ArrayList<ArrayList<Pair>> adj) {
        
        visited[node] = 1;
        
        for(int i=0; i<adj.get(node).size(); i++) {
            
            int v = adj.get(node).get(i).node;
            
            if(visited[v] == 0) {
                dfs(v, visited, st, adj);
            }
        }
        
        st.add(node);
    }

	public int[] shortestPath(int N,int M, int[][] edges) {
		//Code here
		
		
		ArrayList<ArrayList<Pair>> adj = new ArrayList<>();
		
		for(int i=0; i<N; i++) {
		    adj.add(new ArrayList<Pair>());
		}
		
		for(int i=0; i<M; i++) {
		    Pair pr = new Pair(edges[i][1], edges[i][2]);
		    
		    adj.get(edges[i][0]).add(pr);
		}
		
		Stack<Integer> st = new Stack<>();
		int visited[] = new int[N];
		
		
		for(int i=0; i<N; i++) {
		    if(visited[i] == 0) {
		        dfs(i, visited, st, adj);
		    }
		}
		
		int dist[] = new int[N];
		
		for(int i=0; i<N; i++) {
		    dist[i] = (int)(1e9);
		}
		
		dist[0] = 0;
		
		while(!st.isEmpty()) {
		    int node = st.peek();
		    st.pop();
		    
		    for(int i=0; i<adj.get(node).size(); i++) {
		        
		        int child = adj.get(node).get(i).node;
		        int distance = adj.get(node).get(i).dist;
		        
		        if(dist[node] + distance < dist[child]) {
		            dist[child] = distance + dist[node];
		        }
		    }
		}
		
	
		
		for(int i=0; i<N; i++) {
		    if(dist[i] == 1e9) dist[i] = -1;
		}
		
		return dist;
		   
	}
}

```


## Complexity Analysis:

### Time Complexity: O(N + M) + O(N + M)

### Space Complexity: (N)


## Approach - 2 - Toposort with BFS

```java

class Solution {
  public:
  
     void toposort(vector<pair<int, int>> adj[], vector<int> &inDegree, vector<int> &topo) {
        
        queue<int> que;
        
        for(int i=0; i<inDegree.size(); i++) {
            if(inDegree[i] == 0) {
                que.push(i);
            }
        }
        
        while(!que.empty()) {
            int node = que.front();
            que.pop();
            topo.push_back(node);
            
            for(auto adjNode : adj[node]) {
                int child = adjNode.first;
                
                inDegree[child] --;
                
                if(inDegree[child] == 0) {
                    que.push(child);
                }
            }
        }
         
         
     }
     vector<int> shortestPath(int n,int m, vector<vector<int>>& edges){
        
        vector<pair<int, int>> adj[n];
        vector<int> inDegree(n, 0);
        
        for(auto edge : edges) {
            adj[edge[0]].push_back({edge[1], edge[2]});
            inDegree[edge[1]] ++;
        }
        
        vector<int> topo;
        
        toposort(adj, inDegree, topo);
        
        vector<int> dist(n, 1e9);
        
        int index = 0;
        
        dist[topo[index]] = 0;
        
        while(index < n) {
            int node = topo[index++];
            
            for(auto adjNode : adj[node]) {
                
                int child = adjNode.first;
                int distance = adjNode.second;
                
                
                if(dist[node] + distance < dist[child]) {
                    dist[child] = dist[node] + distance;
                }
            }
        }
        
        for(int i=0; i<n; i++){
            if(dist[i] == 1e9) {
                dist[i] = -1;
            }
        }
        
        
        return dist;
    }
};

```
## Complexity Analysis:

### Time Complexity: O(V + E) + O(V + E)

### Space Complexity: (V)
