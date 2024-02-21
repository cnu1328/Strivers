# Subset Sum Equal to K

[Problem Link](https://www.codingninjas.com/studio/problems/subset-sum-equal-to-k_1550954?utm_source=striver&utm_medium=website&utm_campaign=a_zcoursetuf&leftPanelTabValue=PROBLEM)


## Recurssion

```Java

import java.util.* ;
import java.io.*; 
public class Solution {

    static boolean helper(int n, int sum, int k, int[] arr) {
        if(n < 0) return false;

        if(sum > k) return false;

        if(k == sum) return true;

        

        boolean take = helper(n-1, sum + arr[n], k, arr);
        boolean notTake = helper(n-1, sum, k, arr);

        boolean flag = (take || notTake);

        

        return flag;
    }
    
    public static boolean subsetSumToK(int n, int k, int arr[]){

        return helper(n-1, 0, k, arr);
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

    static boolean helper(int n, int sum, int k, int[] arr, int[][] dp) {
        if(n < 0) return false;

        if(sum > k) return false;

        if(k == sum) return true;

        if(dp[n][sum] != -1) {
            if(dp[n][sum] == 1) return true;
            return false;
        }

        boolean take = helper(n-1, sum + arr[n], k, arr, dp);
        boolean notTake = helper(n-1, sum, k, arr, dp);

        boolean flag = (take || notTake);

        if(flag) dp[n][sum] = 1;
        else dp[n][sum] = 0;

        return flag;
    }
    
    public static boolean subsetSumToK(int n, int k, int arr[]){
        int dp[][] = new int[n][k+1];

        for(int i=0; i<n; i++) {
            for(int j = 0; j<=k; j++) {
                dp[i][j] = -1;
            }
        }
        return helper(n-1, 0, k, arr, dp);
    }
}

```


## Complexity Analysis

### Time Complexity: O(N);

### Space Complexity: O(N*M)


