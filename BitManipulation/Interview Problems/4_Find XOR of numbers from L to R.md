# Find XOR of numbers from L to R.

[Problem Link](https://www.geeksforgeeks.org/problems/find-xor-of-numbers-from-l-to-r/1)

## Approach - 1

1. First know to find the Xor of any number
2. Now, Find the xor of (R)
3. Find the xor of (L-1)
4. return the xor(r) - xor(l-1) ( is our answer)

```c++

class Solution {
  public:

    int solve(int num) {

        if(num%4 == 0) return num;

        else if(num%4 == 1) return 1;

        else if(num %4 == 2) return num + 1;

        else return 0;
    }

    int findXOR(int l, int r) {
        return solve(r) ^ solve(l-1);
    }
};

```

## Complexity Analysis:

### Time Complexity: O(1)

### Space Complexity: (1)
