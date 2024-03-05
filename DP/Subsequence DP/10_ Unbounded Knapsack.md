# Unbounded Knapsack

[Problem Link](https://www.codingninjas.com/studio/problems/unbounded-knapsack_1215029?utm_source=striver&utm_medium=website&utm_campaign=a_zcoursetuf&leftPanelTabValue=PROBLEM)

## Recurssion

1. Every Item has infinite supply, think of base case when n == 0

```Java

public class Solution {

    static int solve(int n, int w, int[] profit, int[] weight) {

        if(w == 0) return 0;

        if(n == 0) {
            if(w%weight[n] == 0) return (w/weight[n])*profit[n];

            return 0;
        }


        int notTake = solve(n-1, w, profit, weight);
        int take = Integer.MIN_VALUE;

        if(weight[n] <= w) {

            take = profit[n] + solve(n, w - weight[n], profit, weight);
        }

        return Math.max(notTake, take);
    }
    public static int unboundedKnapsack(int n, int w, int[] profit, int[] weight) {
        return solve(n-1, w, profit, weight);
    }
}

```

## Complexity Analysis:

### Time Complexity: O(2^N)

### Space Complexity: O(N) (stack space)

## Memoization

```Java

public class Solution {

    static int solve(int n, int w, int[] profit, int[] weight, int[][] dp) {

        if(w == 0) return 0;

        if(n == 0) {
            if(w%weight[n] == 0) return (w/weight[n])*profit[n];

            return 0;
        }

        if(dp[n][w] != -1) return dp[n][w];


        int notTake = solve(n-1, w, profit, weight, dp);


        int take = Integer.MIN_VALUE;

        if(weight[n] <= w) {

            take = profit[n] + solve(n, w - weight[n], profit, weight, dp);
        }

        return dp[n][w] = Math.max(notTake, take);
    }
    public static int unboundedKnapsack(int n, int w, int[] profit, int[] weight) {
        int dp[][] = new int[n][w+1];

        for(int i=0; i<n; i++) {
            for(int j=0; j<=w; j++) {
                dp[i][j] = -1;
            }
        }

        return solve(n-1, w, profit, weight, dp);
    }
}


```

## Complexity Analysis:

### Time Complexity: O(N\*W)

### Space Complexity: O(N\*W) + O(N) (stack space)

## Tabulation

```Java

public class Solution {


    public static int unboundedKnapsack(int n, int w, int[] profit, int[] weight) {
        int dp[][] = new int[n][w+1];

        for(int i=0; i<=w; i++) {

            if(i%weight[0] == 0)
                dp[0][i] = (i/weight[0])*profit[0];
        }

        for(int i=1; i<n; i++) {
            for(int j=1; j<=w; j++) {
                int notTake = dp[i-1][j];

                int take = 0;

                if(weight[i] <= j) {
                    take = profit[i] + dp[i][j - weight[i]];
                }

                dp[i][j] = Math.max(notTake, take);
            }
        }

        return dp[n-1][w];

    }
}


```

## Complexity Analysis:

### Time Complexity: O(N\*W)

### Space Complexity: O(N\*W) 

## Space Optimization



```Java

public class Solution {

    
    public static int unboundedKnapsack(int n, int w, int[] profit, int[] weight) {
        int prev[] = new int[w+1];
        int curr[] = new int[w+1];

        for(int i=0; i<=w; i++) {

            if(i%weight[0] == 0)
                prev[i] = (i/weight[0])*profit[0];
        }

        for(int i=1; i<n; i++) {
            for(int j=1; j<=w; j++) {
                int notTake = prev[j];

                int take = 0;

                if(weight[i] <= j) {
                    take = profit[i] + curr[j - weight[i]];
                }

                curr[j] = Math.max(notTake, take);
            }

            prev = curr;
        }

        return prev[w];
        
    }
}


```

## Complexity Analysis:

### Time Complexity: O(N\*W)

### Space Complexity: O(N)

## Space Optimization with Single Array

```Java

public class Solution {

    
    public static int unboundedKnapsack(int n, int w, int[] profit, int[] weight) {
        int prev[] = new int[w+1];

        for(int i=0; i<=w; i++) {

            if(i%weight[0] == 0)
                prev[i] = (i/weight[0])*profit[0];
        }

        for(int i=1; i<n; i++) {
            for(int j=1; j<=w; j++) {
                int notTake = prev[j];

                int take = 0;

                if(weight[i] <= j) {
                    take = profit[i] + curr[j - weight[i]];
                }

                prev[j] = Math.max(notTake, take);
            }
        }

        return prev[w];
        
    }
}


```

## Complexity Analysis:

### Time Complexity: O(N\*W)

### Space Complexity: O(N)



