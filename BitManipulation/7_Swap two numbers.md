# Swap two numbers

[Problem Link](https://www.geeksforgeeks.org/problems/swap-two-numbers3844/1)

## Approach - 1

1. First, do a = a ^ b
2. Second, b = a ^ b
3. next, a = a ^ b

```c++

class Solution{
public:
    pair<int, int> get(int a, int b){
        a = a ^ b;
        b = a ^ b;
        a = a ^ b;

        return {a, b};
    }
};

```

## Complexity Analysis:

### Time Complexity: O(1)

### Space Complexity: (1)
