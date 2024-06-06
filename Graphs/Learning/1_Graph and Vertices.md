# Graph and Vertices

[Problem Link](https://www.geeksforgeeks.org/problems/graph-and-vertices/1)

## Approach 

1. For every vertex we can connect n-1 other vertices (consider self edge not exit) => n * (n-1)
2. Divide it by 2, to aviod the double counting, since it is undirected graph
3. n*(n-1)/2
4. finally we get total number of edge count
5. return 2^edge count, because we can pick or not pick an edge

```Java

class Solution {
  public:
    long long count(int n) {
        // your code here
        
        return 1LL << (n*(n-1)/2);
    }
};

```

## Complexity Analysis:

### Time Complexity: O(1)

### Space Complexity: O(1)


