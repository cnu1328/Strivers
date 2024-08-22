# Floyd Warshall

[Problem Link](https://www.geeksforgeeks.org/problems/implementing-floyd-warshall2042/1)

## Approach - 1

1. **Floyd Warshall algorithm** is a **multi-source shortest path algorithm** and it helps to **detect negative cycles** as well. The shortest path between node u and v necessarily means the path(from u to v) for which the sum of the edge weights is minimum.

![image](https://github.com/user-attachments/assets/1f4bd3ce-4d2d-45ed-bda8-c3d6fe0229db)

2. matrix[i][j] =min(matrix[i][j], matrix[i ][k]+matrix[k][j]), where i = source node, j = destination node, and k = the node via which we are reaching from i to j.

<img width="743" alt="image" src="https://github.com/user-attachments/assets/17d373e4-8e60-4783-9b14-54f8b2507cb8">

<img width="740" alt="image" src="https://github.com/user-attachments/assets/0f8ed954-1f80-41c4-9b16-5b2c69439ae1">

3. Convert undirected edge to

![image](https://github.com/user-attachments/assets/609daf69-7408-4a09-85fa-a5e561658afc)

4. Detect Negative cycle

<img width="761" alt="image" src="https://github.com/user-attachments/assets/5270c965-1555-4d8a-9be3-0aa21051811b">

5. What will happen if we will apply Dijkstra’s algorithm for this purpose?

   - If the graph has a negative cycle: It will give TLE error in that case.

   - If the graph does not contain a negative cycle: we will apply Dijkstra’s algorithm for every possible node to make it work like a multi-source shortest path algorithm like Floyd Warshall.

   - we apply Dijkstra’s algorithm for the same purpose the time complexity reduces to O(V*(E*logV)) (where v = no. of vertices).

```c++

class Solution {
  public:
	void shortest_distance(vector<vector<int>>&matrix){
	    int n = matrix.size();

	    for(int i=0; i<n; i++) {
	        for(int j=0; j<n; j++) {
	            if(matrix[i][j] == -1) {
	                matrix[i][j] = 1e9;
	            }
	        }
	    }

	    for(int k = 0; k < n; k++) {
	        for(int i=0; i<n; i++) {
	            for(int j=0; j<n; j++) {

	                if(matrix[i][k] + matrix[k][j] < matrix[i][j]) {
	                    matrix[i][j] = matrix[i][k] + matrix[k][j];
	                }
	            }
	        }
	    }

	    for(int i=0; i<n; i++) {
	        for(int j=0; j<n; j++) {
	            if(matrix[i][j] == 1e9) {
	                matrix[i][j] = -1;
	            }
	        }
	    }
	}
};

```

## Complexitiy Analysis:

### Time Complexity : O(V ^ 3)

### Space Compleixty : O(V ^ 2)
