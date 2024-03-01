# 0/1 KanpSack

[Problem Link](https://www.codingninjas.com/studio/problems/0-1-knapsack_920542?utm_source=striver&utm_medium=website&utm_campaign=a_zcoursetuf)

## Recurrsion

1. Try out all possible ways to get maximum value by stealing items.
2. Think of base case interm of single value, when n == 0 think, a robber will take the element or not.
3. If weight is equal to zero, the bag is fulled.

```Java

import java.util.* ;
import java.io.*;

public class Solution{

    static int knap(int ind, int wt, int[] weight, int[] value) {

        if(wt == 0) return 0;


        if(ind == 0) {
            if(weight[ind] <= wt) return value[ind];

            return 0;

        }

        int take = 0;

        if(weight[ind] <= wt) {
            take = value[ind] + knap(ind - 1, wt - weight[ind], weight, value);
        }

        int notTake = knap(ind-1, wt, weight, value);

        return Math.max(take, notTake);
    }

    static int knapsack(int[] weight, int[] value, int n, int maxWeight) {

        return knap(n-1, maxWeight, weight, value);

    }
}

```

## Complexity Analysis:

### Time Complexity: O(2^N)

### Space Complexity: O(N) (Stack Space)

## Memoization

1. use dp array and solve

```Java

import java.util.* ;
import java.io.*;

public class Solution{

    static int knap(int ind, int wt, int[] weight, int[] value, int[][] dp) {

        if(wt == 0) return 0;


        if(ind == 0) {
            if(weight[ind] <= wt) return value[ind];

            return 0;

        }

        if(dp[ind][wt] != -1) return dp[ind][wt];

        int take = 0;

        if(weight[ind] <= wt) {
            take = value[ind] + knap(ind - 1, wt - weight[ind], weight, value, dp);
        }

        int notTake = knap(ind-1, wt, weight, value, dp);

        return dp[ind][wt] = Math.max(take, notTake);
    }

    static int knapsack(int[] weight, int[] value, int n, int maxWeight) {

        int dp[][] = new int[n][maxWeight + 1];

        for(int i=0; i<n; i++) {
            Arrays.fill(dp[i], -1);
        }

        return knap(n-1, maxWeight, weight, value, dp);

    }
}

```

## Complexity Analysis:

### Time Complexity: O(N\*W)

### Space Complexity: O(N\*W) + O(N) (Stack Space)

## Tabulation

```Java

import java.util.* ;
import java.io.*;

public class Solution{
    static int knapsack(int[] weight, int[] value, int n, int maxWeight) {
        int dp[][] = new int[n][maxWeight + 1];

        for(int i=weight[0]; i<=maxWeight; i++) {
            dp[0][i] = value[0];
        }

        for(int i=1; i<n; i++) {
            for(int j=1; j<=maxWeight; j++) {

                int notTake = dp[i-1][j];
                int take = 0;

                if(weight[i] <= j) {
                    take = value[i] + dp[i-1][j - weight[i]];
                }

                dp[i][j] = Math.max(take, notTake);
            }
        }

        return dp[n-1][maxWeight];

    }
}

```

## Complexity Analysis:

### Time Complexity: O(N\*W)

### Space Complexity: O(N\*W)

## Space Optimization

```Java

import java.util.* ;
import java.io.*;

public class Solution{
    static int knapsack(int[] weight, int[] value, int n, int maxWeight) {
        int prev[] = new int[maxWeight + 1];
        int curr[] = new int[maxWeight + 1];

        for(int i=weight[0]; i<=maxWeight; i++) {
            prev[i] = value[0];
        }

        for(int i=1; i<n; i++) {
            for(int j=1; j<=maxWeight; j++) {

                int notTake = prev[j];
                int take = 0;

                if(weight[i] <= j) {
                    take = value[i] + prev[j - weight[i]];
                }

                curr[j] = Math.max(take, notTake);
            }

            for(int j=0; j<=maxWeight; j++) {
                prev[j] = curr[j];
            }
        }

        return prev[maxWeight];



    }
}

```

## Complexity Analysis:

### Time Complexity: O(N\*W)

### Space Complexity: O(W)

## One Array Optimizatin

```Java


import java.util.* ;
import java.io.*;

public class Solution{
    static int knapsack(int[] weight, int[] value, int n, int maxWeight) {
        int prev[] = new int[maxWeight + 1];


        for(int i=weight[0]; i<=maxWeight; i++) {
            prev[i] = value[0];
        }

        for(int i=1; i<n; i++) {
            for(int j=maxWeight; j>0; j--) {

                int notTake = prev[j];
                int take = 0;

                if(weight[i] <= j) {
                    take = value[i] + prev[j - weight[i]];
                }

                prev[j] = Math.max(take, notTake);
            }


        }

        return prev[maxWeight];



    }
}

```

## Complexity Analysis:

### Time Complexity: O(N\*W)

### Space Complexity: O(W)
