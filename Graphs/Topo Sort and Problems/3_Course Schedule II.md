# Course Schedule II

[Problem Link](https://leetcode.com/problems/course-schedule-ii/)

## Approach - Using Topological Sort - DFS

```Java

class Solution {
public:
    vector<int> findOrder(int numCourses, vector<vector<int>>& prerequisites) {
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
        
        if(ans.size() == numCourses) return ans;
        return {};
    
    }
};

```

## Complexity Analysis:

### Time Complexity: (V + E)

### Space Complexity: (V)