# Minimum Spanning Tree

[Problem Link](https://www.geeksforgeeks.org/problems/minimum-spanning-tree/1)

## Approach - 1 - Prims Algorithm

1. Prims Algorithm is an algorithm which is used to find the MST
2. The requirements to write Prims Algo are
   - Priority queue
   - Visited array

<img width="742" alt="image" src="https://github.com/user-attachments/assets/c72c6e35-fe00-4cea-a5c8-0275e13a8698">

3. Dry Run

<img width="743" alt="image" src="https://github.com/user-attachments/assets/1769e39f-328e-4b86-8309-b6512124bb82">

4. Return the answer

```c++

#define pr pair<int, pair<int, int>>

class Solution
{
	public:
    int spanningTree(int V, vector<vector<int>> adj[])
    {
        vector<bool> visited(V, false);
        vector<pair<int, int>> mst;

        priority_queue<pr, vector<pr>, greater<pr>> mheap;

        mheap.push({0, {0, -1}});
        int ans = 0;

        // E times traverses
        while(!mheap.empty()) {

            // Log E
            auto prr = mheap.top();
            mheap.pop();

            int dist = prr.first;
            int node = prr.second.first;
            int parent = prr.second.second;

            if(visited[node]) continue;

            if(parent != -1 && !visited[node]) {
                ans += dist;
                mst.push_back({node, parent});
            }

            visited[node] = true;

            // E Log E
            for(auto child : adj[node]) {
                int childNode = child[0];
                int distance = child[1];

                if(!visited[childNode]) {
                    mheap.push({distance, {childNode, node}});
                }

            }
        }

        // Total Time = E Log E + E Log E = E Log E

        return ans;
    }
};


```

## Complexitiy Analysis:

### Time Complexity : O(E Log E)

### Space Compleixty : O(E)
