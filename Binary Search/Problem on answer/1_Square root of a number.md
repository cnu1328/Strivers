# Square root of a number

[Problem Link](https://www.geeksforgeeks.org/problems/square-root/0)

## Approach - 1 - Brute Force

1. Perform linear Search and check i \* i <= n, then store the i in answer variable
2. return the answer

```Java

public static int floorSqrt(int n) {
    int ans = 0;
    // linear search on the answer space
    for (long i = 1; i <= n; i++) {
        long val = i * i;
        if (val <= (long) n) {
            ans = (int) i;
        } else {
            break;
        }
    }
    return ans;
}

```

## Complexity Analysis:

### Time Complexity: O(N)

### Space Complexity: O(1)

## Approach - 2 - use Built In Square Function

1. Use built-in square function

```Java

public static int floorSqrt(int n) {
    int ans = (int) Math.sqrt(n);
    return ans;
}

```

## Complexity Analysis:

### Time Complexity: O(Log N)

### Space Complexity: O(1)

## Approach - 3 - Using Binary Search

1. Perform binary search on the answer, check for every element if mid \* mid <= given n then make low = mid + 1
2. other wise high = mid - 1

```Java

class Solution {
  public:
    long long int floorSqrt(long long int n) {
        // Your code goes here
        
        long long int low = 0, high = n;
        long long int ans;
        
        while(low <= high) {
            long long int mid = low + (high - low) / 2;
            
            long long int value = mid * mid;
            
            if(value <= n) {
                ans = mid;
                low = mid + 1;
            }
            
            else {
                high = mid - 1;
            }
            
        }
        
        return ans;
    }
};

```

## Complexity Analysis:

### Time Complexity: O(Log N)

### Space Complexity: O(1)
