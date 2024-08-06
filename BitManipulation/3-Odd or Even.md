# Odd or Even

[Problem Link](https://www.geeksforgeeks.org/problems/odd-or-even3618/1)

## Approach - 1

1. Check if even = N & 1 == 0
2. odd N & 1 = 1

```c++


class Solution {
  public:
    string oddEven(int n) {
        if(n&1) {
            return "odd";
        }

        return "even";
    }
};
```

## Complexity Analysis:

### Time Complexity: O(1)

### Space Complexity: (1)
