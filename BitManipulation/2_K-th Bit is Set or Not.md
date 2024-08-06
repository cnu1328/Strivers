# K-th Bit is Set or Not

[Problem LInk](https://www.geeksforgeeks.org/problems/check-whether-k-th-bit-is-set-or-not-1587115620/1)

## Approach - 1

1. Right shift the given number by K and perform and operation

```c++

class Solution {
  public:
    bool checkKthBit(int n, int k) {

        return ((n >> k) & 1);
    }
};


```

## Complexity Analysis:

### Time Complexity: O(1)

### Space Complexity: (1)
