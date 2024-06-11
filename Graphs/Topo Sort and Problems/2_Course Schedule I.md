# Course Schedule I

[Problem Link](https://leetcode.com/problems/course-schedule/)

## Approach - 1 - Using DFS

1. This problem is equivalent to finding if a cycle exists in a directed graph. If a cycle exists, no topological ordering exists and therefore it will be impossible to take all courses.
2. Find a cycle if exists in the directed graph, if exists return false
3. otherwise return true

```Java

class Solution {
public:
    
    bool dfs(int node, vector<int> &visited, vector<int> &path, vector<int> adj[]) {
        visited[node] = 1;
        path[node] = 1;
        
        for(int child : adj[node]) {
            if(!visited[child]) {
                if(dfs(child, visited, path, adj) == true) 
                    return  true;
            }
            
            else if(path[child]) return true;
        }
        
        
        path[node] = 0;
        return false;
    }
    
    bool canFinish(int numCourses, vector<vector<int>>& pre) {
        
        vector<int> visited(numCourses, 0);
        vector<int> path(numCourses, 0);
        
        vector<int> adj[numCourses];
        
        for(int i=0; i<pre.size(); i++) {
            adj[pre[i][1]].push_back(pre[i][0]);
        }
        
        for(int node=0; node < numCourses; node++) {
            if(!visited[node]) {
                if(dfs(node, visited, path,adj) == true) return false;
            }
        }
        
        return true;
    }
};


```

## Complexity Analysis:

### Time Complexity: (V + E)

### Space Complexity: (V)

## Approach - 1 - Using Topology Sort - BFS

1. This problem is equivalent to finding if a cycle exists in a directed graph. If a cycle exists, no topological ordering exists and therefore it will be impossible to take all courses.
2. Implement Topological sort algorithm


```Java

class Solution {
public:
    bool canFinish(int numCourses, vector<vector<int>>& prerequisites) {
        
        vector<int> inDegree(numCourses, 0);
        vector<int> adj[numCourses];
        
        for(int i=0; i < prerequisites.size(); i++) {
            adj[prerequisites[i][1]].push_back(prerequisites[i][0]);   
        }
        
        for(int i=0; i<numCourses; i++) {
            
            for(int node : adj[i]) {
                inDegree[node]++;
            }
        }
        
        queue<int> que;
        
        for(int i=0; i<numCourses; i++) {
            if(inDegree[i] == 0) {
                que.push(i);
            }
        }
        
        int cnt = 0;
        
        while(!que.empty()) {
            int node = que.front();
            que.pop();
            cnt++;
            
            for(int child : adj[node]) {
                inDegree[child]--;
                
                if(inDegree[child] == 0) {
                    que.push(child);
                }
            }
            
        }
        
        if(cnt == numCourses) return true;
        return false;
        
    }
};

```

## Complexity Analysis:

### Time Complexity: (V + E)

### Space Complexity: (V)
