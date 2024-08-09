# Introduction to Trees

[Problem Link](https://www.geeksforgeeks.org/problems/introduction-to-trees/1)

## Approach - 1

1. In each level we have
   - 1 - 1 node - 2^0
   - 2 - 2 nodes - 2^1
   - 3 - 4 nodes - 2^2
   - 4 - 8 nodes - 2^3
2. return (1 << (i - 1))

```c++
class Solution {
  public:
    int countNodes(int i) {

        return (1<<(i-1));
    }
};

```

## Complexitiy Analysis:

### Time Complexity : O(N)

### Space Compleixty : O(N)
