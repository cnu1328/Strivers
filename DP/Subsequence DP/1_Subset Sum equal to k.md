# Subset Sum Equal to K

[Problem Link](https://www.codingninjas.com/studio/problems/subset-sum-equal-to-k_1550954?utm_source=striver&utm_medium=website&utm_campaign=a_zcoursetuf&leftPanelTabValue=PROBLEM)

## Recurssion

```Java

import java.util.* ;
import java.io.*;
public class Solution {

    static boolean solve(int n, int target, int []arr) {

        if(target == 0) return true;

        if(n == 0) return (arr[n] == target);

        boolean notTake = solve(n-1, target, arr);

        boolean Take = false;

        if(arr[n] <= target) {
            Take = solve(n-1, target - arr[n], arr);
        }

        return (notTake || Take);
    }
    public static boolean subsetSumToK(int n, int k, int arr[]){

        return solve(n-1, k, arr);
    }
}



```

## Complexity Analysis

### Time Complexity: O(2^N);

### Space Complexity: O(N)

## Memoization

```Java

import java.util.* ;
import java.io.*;
public class Solution {

    static boolean solve(int n, int target, int []arr, int[][] dp) {

        if(target == 0) return true;

        if(n == 0) return (arr[n] == target);

        if(dp[n][target] != -1) {
            if(dp[n][target] == 1) return true;
            return false;
        }

        boolean notTake = solve(n-1, target, arr, dp);

        boolean Take = false;

        if(arr[n] <= target) {
            Take = solve(n-1, target - arr[n], arr, dp);
        }

        boolean flag = (Take || notTake);

        if(flag) dp[n][target] = 1;
        else dp[n][target] = 0;

        return flag;
    }
    public static boolean subsetSumToK(int n, int k, int arr[]){
        int dp[][] = new int[n][k+1];

        for(int i = 0; i<n; i++) {
            for(int j=0; j<=k ;j++) {
                dp[i][j] = -1;
            }
        }
        return solve(n-1, k, arr, dp);
    }
}


```

## Complexity Analysis

### Time Complexity: O(N\*target);

### Space Complexity: O(N\*target) + O(N)

## Tabulation

```C++

#include <bits/stdc++.h>
bool subsetSumToK(int n, int k, vector<int> &arr) {
    vector<vector<bool>> dp(n, vector<bool> (k+1, false));

    for(int i=0; i<n; i++) {
        dp[i][0] = true;
    }

    dp[0][arr[0]] = true;

    for(int i = 1; i<n; i++) {
        for(int target = 1; target <= k; target++) {

            bool notTake = dp[i-1][target];

            bool Take = false;

            if(arr[i] <= target) {
                Take = dp[i-1][target - arr[i]];
            }

            dp[i][target] = (Take || notTake);
        }
    }

    return dp[n-1][k];
}

```

## Complexity Analysis

### Time Complexity: O(N\*target)

### Space Complexity: O(N\*target)

## Space Optimization

```C++



```

## Complexity Analysis

### Time Complexity: O(N\*target);

### Space Complexity: O(target)
