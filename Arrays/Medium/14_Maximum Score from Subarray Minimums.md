# Maximum Score from Subarray Minimums

[Problem Link](https://www.geeksforgeeks.org/problems/max-sum-in-sub-arrays0824/0)

## Approach - 1

1. Maximum sum of two consecutive element in array is the answer

```c++

class Solution {

    public static long pairWithMaxSum(long arr[], long N) {
        long ans = 0;

        for(int i=1; i<arr.length; i++) {
            ans = Math.max(ans, arr[i] + arr[i-1]);
        }

        return ans;
    }
}

```

## Complexity Analysis:

### Time Complexity: O(N)

### Space Complexity: (1)
