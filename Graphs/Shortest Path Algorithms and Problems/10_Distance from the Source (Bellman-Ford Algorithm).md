# Distance from the Source (Bellman-Ford Algorithm)

[Problem Link](https://www.geeksforgeeks.org/problems/distance-from-the-source-bellman-ford-algorithm/1)

## Approach - 1

1. **The bellman-Ford algorithm** helps to find the shortest distance from the source node to all other nodes. But, we have already learned Dijkstra's algorithm (Dijkstra's algorithm article link) to fulfill the same purpose. Now, the question is how this algorithm is different from Dijkstra's algorithm.

2. While learning Dijkstra's algorithm, we came across the following two situations, where Dijkstra's algorithm failed:

   - If the graph contains negative edges.
   - If the graph has a negative cycle (In this case Dijkstra's algorithm fails to minimize the distance, keeps on running, and goes into an infinite loop. As a result it gives TLE error).

3. **Negative Cycle**: A cycle is called a negative cycle if the sum of all its weights becomes negative. The following illustration is an example of a negative cycle:

![image](https://github.com/user-attachments/assets/fa340c7d-1c4d-49f6-9ad3-6ade4cbeaaff)

4. Bellman-Ford's algorithm successfully solves these problems. It works fine with negative edges as well as it is able to detect if the graph contains a negative cycle.

5. But this algorithm is only applicable for directed graphs. In order to apply this algorithm to an undirected graph, we just need to convert the undirected edges into directed edges like the following:

![image](https://github.com/user-attachments/assets/5f57b295-ce25-4b8e-912f-e7cb028a32ef)

## Intuition

1. In this algorithm, the edges can be given in any order. The intuition is to relax all the edges for N-1( N = no. of nodes) times sequentially. After N-1 iterations, we should have minimized the distance to every node.

2. This process of updating the distance is called the relaxation of edges.

**Two follow-up questions about the algorithm: Why do we need exact N-1 iterations?**

<img width="741" alt="image" src="https://github.com/user-attachments/assets/d5b9cb7c-a392-43a4-b683-910a8875dd6e">

<img width="740" alt="image" src="https://github.com/user-attachments/assets/62bb8715-8c6f-4a9a-bcfe-e5bc0436a316">

<img width="733" alt="image" src="https://github.com/user-attachments/assets/a51bb68d-c497-45b6-887d-6976eb45548b">

```c++

class Solution {
  public:

    vector<int> bellman_ford(int V, vector<vector<int>>& edges, int S) {

        vector<int> dist(V, 1e8);
        dist[S] = 0;

        // perform N-1 Iterations
        for(int i=0; i<V; i++) {
            for(auto edge : edges) {
                int parent = edge[0];
                int child = edge[1];
                int weight = edge[2];

                // relax the edges
                if(dist[parent] != 1e8 && dist[parent] + weight < dist[child]) {
                    dist[child] = dist[parent] + weight;
                }

            }
        }

        // check for any negative cycle
        for(auto edge : edges) {
            int parent = edge[0];
            int child = edge[1];
            int weight = edge[2];

            if(dist[parent] != 1e8 && dist[parent] + weight < dist[child]) {
               return {-1};
            }

        }

        return dist;
    }
};

```

## Complexitiy Analysis:

### Time Complexity : O(V \* E)

### Space Compleixty : O(V)
