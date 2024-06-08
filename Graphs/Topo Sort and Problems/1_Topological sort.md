# Topological sort

[Problem Link](https://www.geeksforgeeks.org/problems/topological-sort/1)

## Approach - Using DFS

1. Linear ordering of vetices such that if there is an edge between u and v, u should appear before v in the ordering
2. lets take example
    - 1 -> 2 -> 3 -> 4 -> 5
                       -> 6
    - The ordering will be like 1 2 3 4 5 6 or 1 2 3 4 6 5
3. Observe Carefully, that if the dfs call is finished then the number is added into the ordering
4. But we get in reverse order, to set it out, use stack
5. after comleting one dfs call push that node to stack
6. after all dfs calls, push stack elements to vector and return the answer

```Java

class Solution
{
    
    private:
        void dfs(int node, int visited[], stack<int> &st, vector<int> adj[]) {
           
            visited[node] = 1;
    
    
            for(int child : adj[node]) {
                if(!visited[child]) {
                    dfs(child, visited, st, adj);
                }
            }
            
            st.push(node);
        }
     
	public:
	//Function to return list containing vertices in Topological order. 
	vector<int> topoSort(int V, vector<int> adj[]) 
	{
	    // code here
	    stack<int> st;
	    int visited[V] = {0}; 
	    
	    for(int i=0; i<V; i++) {
	        if(!visited[i]) {
	            dfs(i, visited, st, adj);
	        }
	    }
	    
	    vector<int> ans;
	    
	    while(!st.empty()) {
	        ans.push_back(st.top());
	        st.pop();
	    }
	    
	    return ans;
	}
};


```

## Complexity Analysis:

### Time Complexity: O(V + E)

### Space Complexity: (V)


## Approach - Using BFS (Khan's algorithm)

1. First count the indegree of each node
2. If indegree of any node is zero, then push into the queue
3. Traverse the queue, pop element from queue, and push that element into ans
4. Check for adjatancy nodes, and reduces its indegree, if indegree of any node becomes zero then insert into the queue


```Java

class Solution
{
	public:
	//Function to return list containing vertices in Topological order. 
	vector<int> topoSort(int V, vector<int> adj[]) 
	{
	    // code here
	    
	    
	    int inDegree[V] = {0};
	    
	    for(int node=0; node<V; node++) {
	        for(int child : adj[node]) {
	            inDegree[child]++;
	        }
	    }
	    
	    queue<int> que;
	    
	    for(int node =0; node <V; node++) {
	        if(inDegree[node] == 0) {
	            que.push(node);
	        } 
	    }
	    
	    vector<int> ans;
	    
	    while(!que.empty()) {
	        int node = que.front();
	        que.pop();
	        ans.push_back(node);
	        
	        for(int child : adj[node]) {
	            inDegree[child]--;
	            if(inDegree[child] == 0) {
	                que.push(child);
	            }
	        }
	    }
	    
	    return ans;
	}
};

```


## Complexity Analysis:

### Time Complexity: O(V + E)

### Space Complexity: (V)


