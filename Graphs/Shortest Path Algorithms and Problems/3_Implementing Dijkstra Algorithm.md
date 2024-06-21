# Implementing Dijkstra Algorithm

[Problem Link](https://www.geeksforgeeks.org/problems/implementing-dijkstra-set-1-adjacency-matrix/1)


## Approach - Using Priority Queue

1. Use Min-Heap Priority Queue, then do the same as BFS traversal
2. first insert source node and its distance to min-heap
3.  For every node, check for its adjacent nodes if the total distance if less than the already existing distance in distance array
4. In that case add the new pair to the priority queue
5. After this, return the distance array

```Java

class Pair {
    int dist, node;
    
    Pair(int _dist, int _node) {
        this.dist = _dist;
        this.node = _node;
    }
}

class Solution
{
    //Function to find the shortest distance of all the vertices
    //from the source vertex S.
    static int[] dijkstra(int V, ArrayList<ArrayList<ArrayList<Integer>>> adj, int S)
    {
        // Write your code here
        
        PriorityQueue<Pair> heap = new PriorityQueue<Pair>((x, y) -> x.dist - y.dist);
        
        heap.add(new Pair(0, S));
        
        int dist[] = new int[V];
        
        for(int i=0; i<V; i++) {
            dist[i] = (int)(1e9);
        }
        
        dist[S] = 0;
        
        while(!heap.isEmpty()) {
            int edgeDist = heap.peek().dist;
            int node = heap.peek().node;
            
            heap.poll();
            
            for(ArrayList<Integer> arr : adj.get(node)) {
                int child = arr.get(0);
                int nodeDistance = arr.get(1);
                
                if(dist[node] + nodeDistance < dist[child]) {
                    dist[child] = dist[node] + nodeDistance;
                    heap.add(new Pair(dist[child], child));
                }
            }
        }
        
        return dist;
        
        
        
    }
}

```

## Complexity Analysis:

### Time Complexity: O(E log V) E -> NO. of Edges, V-> NO. of nodes

### Space Complexity: (V)



## Approach - Queue


```Java


class Pair {
    int dist, node;
    
    Pair(int _dist, int _node) {
        this.dist = _dist;
        this.node = _node;
    }
}

class Solution
{
    //Function to find the shortest distance of all the vertices
    //from the source vertex S.
    static int[] dijkstra(int V, ArrayList<ArrayList<ArrayList<Integer>>> adj, int S)
    {
        
        Queue<Pair> heap = new LinkedList<>();
        
        heap.add(new Pair(0, S));
        
        int dist[] = new int[V];
        
        for(int i=0; i<V; i++) {
            dist[i] = (int)(1e9);
        }
        
        dist[S] = 0;
        
        while(!heap.isEmpty()) {
            int edgeDist = heap.peek().dist;
            int node = heap.peek().node;
            
            heap.poll();
            
            for(ArrayList<Integer> arr : adj.get(node)) {
                int child = arr.get(0);
                int nodeDistance = arr.get(1);
                
                if(dist[node] + nodeDistance < dist[child]) {
                    dist[child] = dist[node] + nodeDistance;
                    heap.add(new Pair(dist[child], child));
                }
            }
        }
        
        return dist;
        
        
        
    }
}

```


## Approach - Using Set


```Java


class Solution
{
	public:
	//Function to find the shortest distance of all the vertices
    //from the source vertex S.
    vector <int> dijkstra(int V, vector<vector<int>> adj[], int S)
    {
        // Code here
        
        set<pair<int, int>> st;
        
        st.insert({0, S});
        
        vector<int> dist(V, 1e9);
        
        dist[S] = 0;
        
        while(!st.empty()) {
            auto pr = *(st.begin());
            int distance = pr.first;
            int node = pr.second;
            
            st.erase({distance, node});
            
            for(auto child : adj[node]) {
                int adjNode = child[0];
                int adjDist = child[1];
                
                if(dist[node] + adjDist < dist[adjNode]) {
                    
                    if(dist[adjNode] != 1e9) 
                        st.erase({dist[adjNode], adjNode});
                        
                    dist[adjNode] = dist[node] + adjDist;
                    st.insert({dist[adjNode], adjNode});
                }
            }
        }
        
        return dist;
    }
};

```

