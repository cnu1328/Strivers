# Frog Jump

[Problem Link](https://www.codingninjas.com/studio/problems/frog-jump_3621012?utm_source=striver&utm_medium=website&utm_campaign=a_zcoursetuf)

## Intuition

1. As frog jumps either one or two steps forward. make sure write recurssion of f(n-1) and f(n-2)
2. But, in the question it is given that abs(a[index] - a[index-1 | 2]). The absolute value should be minimum.
3. Write recurrsion for it

### Recurssion

```Java

import java.util.* ;
import java.io.*;
public class Solution {


    static int calculateFrog(int index, int heights[]) {

        if(index == 0) {
            return 0;
        }

        int step1 = calculateFrog(index -1, heights) + Math.abs(heights[index] - heights[index-1]);
        int step2 = Integer.MAX_VALUE;
        if(index > 1)
            step2 = calculateFrog(index -2, heights) + Math.abs(heights[index] - heights[index-2]);

        return Math.min(step1, step2);


    }
    public static int frogJump(int n, int heights[]) {

        return calculateFrog(n-1, heights);

    }

}

```

## Complexity Analysis

### Time Complexity: O(2^N)

### Space Complexity: O(stack space)

## Memoization

1. use 1D dp array, and initialize with -1
2. while returning min value in recurssion assgin the value to dp[n]
3. if dp[n] is not equal to -1 return dp[n]

```Java

import java.util.* ;
import java.io.*;
public class Solution {


    static int calculateFrog(int index, int heights[], int dp[]) {

        if(index == 0) {
            return 0;
        }

        if(dp[index] != -1) return dp[index];

        int step1 = calculateFrog(index -1, heights, dp) + Math.abs(heights[index] - heights[index-1]);
        int step2 = Integer.MAX_VALUE;
        if(index > 1)
            step2 = calculateFrog(index -2, heights, dp) + Math.abs(heights[index] - heights[index-2]);

        return dp[index] = Math.min(step1, step2);


    }
    public static int frogJump(int n, int heights[]) {
        int[] dp = new int[n+1];

        for(int i=0; i<=n; i++) {
            dp[i] = -1;
        }
        return calculateFrog(n-1, heights, dp);

    }

}

```

## Complexity Analysis

### Time Complexity: O(N)

### Space Complexity: O(N) + O(stack space)

## Tabulation

### Intuition

1. Declare the dp array
2. initialize the dp array with base cases
3. See the recurssion pattern and replace the funcitons with dp[index]

```Java
import java.util.* ;
import java.io.*;
public class Solution {
    public static int frogJump(int n, int heights[]) {

        int dp[] = new int[n];

        dp[0] = 0;

        for(int i=1; i<n; i++) {
            int fs = dp[i-1] + Math.abs(heights[i] - heights[i-1]);
            int ss = Integer.MAX_VALUE;
            if(i > 1)
                ss = dp[i-2] + Math.abs(heights[i] - heights[i-2]);

            dp[i] = Math.min(fs, ss);
        }

        return dp[n-1];
    }

}
```

## Complexity Analysis

### Time Complexity: O(N)

### Space Complexity: O(N)

## Space Optimization

### Intuition

1. If there are index -1 and index-2 problems are there, we definitely optimize the space.
2. for every curr index element, the problem depending on the solution of prev index and prev prev index.

```Java

import java.util.* ;
import java.io.*;
public class Solution {
    public static int frogJump(int n, int heights[]) {

        int prev = 0, prev2 = 0;

        for(int i=1; i<n; i++) {
            int fs = prev + Math.abs(heights[i] - heights[i-1]);
            int ss = Integer.MAX_VALUE;
            if(i > 1)
                ss = prev2 + Math.abs(heights[i] - heights[i-2]);

            int curr = Math.min(fs, ss);
            prev2 = prev;
            prev = curr;
        }

        return prev;
    }

}
```

## Complexity Analysis

### Time Complexity: O(N)

### Space Complexity: O(1)
