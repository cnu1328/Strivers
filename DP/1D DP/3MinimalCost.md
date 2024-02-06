# Minimal Cost

[Problem Link](https://www.codingninjas.com/studio/problems/minimal-cost_8180930?utm_source=striver&utm_medium=website&utm_campaign=a_zcoursetuf&leftPanelTabValue=PROBLEM)

## Intuition

1. A frog can jump atmost k steps from current step.
2. Our task is to find the minimum cost, where cost is equal to abs(a[i] - a[j])
3. It is same as to frogJump problem, Instead two jumps here we do k jumps means loop

## Recurssion

```Java

public class Solution {

    static int calculateCost(int index, int k, int height[]) {
        if(index == 0) return 0;

        int mini = Integer.MAX_VALUE;

        for(int i=1; i<=k; i++) {
            if(index-i>=0) {
                int val = calculateCost(index-i, k, height) + Math.abs(height[index] - height[index-i]);
                mini = Math.min(mini, val);
            }

        }

        return mini;
    }
    public static int minimizeCost(int n, int k, int []height){

        return calculateCost(n-1, k, height);
    }
}
```

## Complexity Analysis

### Time Complexity : O(N^k)

### Space Complexity: O(stack Space)

## Memoization

1. use dp array to memoize the overlapping problems

```Java

public class Solution {

    static int calculateCost(int index, int k, int height[], int dp[]) {
        if(index == 0) return 0;

        if(dp[index] != -1) return dp[index];

        int mini = Integer.MAX_VALUE;

        for(int i=1; i<=k; i++) {
            if(index-i>=0) {
                int val = calculateCost(index-i, k, height, dp) + Math.abs(height[index] - height[index-i]);
                mini = Math.min(mini, val);
            }

        }

        return dp[index] = mini;
    }
    public static int minimizeCost(int n, int k, int []height){
        int dp[] = new int[n+1];

        for(int i=0; i<n; i++) {
            dp[i] = -1;
        }
        return calculateCost(n-1, k, height, dp);
    }
}
```

## Complexity Analysis

### Time Complexity : O(N\*k)

### Space Complexity: O(N) + O(stack space)

## Tabulation

```Java

public class Solution {
    public static int minimizeCost(int n, int k, int []height){
        int dp[] = new int[n];

        dp[0] = 0;

        for(int i=1; i<n; i++) {
            int mini = Integer.MAX_VALUE;

            for(int j=1; j<=k; j++) {
                if(i-j>=0) {
                    int val = dp[i-j] + Math.abs(height[i] - height[i-j]);
                    mini = Math.min(mini, val);
                }
            }

            dp[i] = mini;
        }

        return dp[n-1];
    }
}
```

## Complexity Analysis

### Time Complexity : O(N*k)

### Space Complexity: O(N)