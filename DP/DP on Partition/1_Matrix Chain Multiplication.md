# Matrix Chain Multiplication

[Problem Link](https://www.geeksforgeeks.org/problems/matrix-chain-multiplication0303/1)

## Approach - Recurrsion

1. This is new Pattern, that DP on partition
2. Here in this problem we try to partition the array into two parts, and find the best possible answer among them

```Java


class Solution{
public:
    int mcm(int i, int j, int arr[], vector<vector<int>> &dp) {
        
        if(i == j) return 0;
        
        
        
        int mini = INT_MAX;
        
        for(int k=i; k<j; k++) {
           int steps = arr[i-1]*arr[k]*arr[j] + mcm(i, k, arr) + mcm(k+1, j, arr);
           mini = min(mini, steps);
           
        }
        
        return mini;
    }

    int matrixMultiplication(int N, int arr[])
    {
        // code here
        
        
        return mcm(1, N-1, arr);
    }
};

```


## Complexity Analysis:

### Time Complexity : O(exponential)
### Space Complexity: O(N)



## Approach - Memoization

```Java


class Solution{
public:
    int mcm(int i, int j, int arr[], vector<vector<int>> &dp) {
        
        if(i == j) return 0;
        
        if(dp[i][j] != -1) return dp[i][j];
        
        int mini = INT_MAX;
        
        for(int k=i; k<j; k++) {
           int steps = arr[i-1]*arr[k]*arr[j] + mcm(i, k, arr, dp) + mcm(k+1, j, arr, dp);
           mini = min(mini, steps);
           
        }
        
        return dp[i][j] = mini;
    }

    int matrixMultiplication(int N, int arr[])
    {
        // code here
        
        vector<vector<int>> dp(N, vector<int> (N, -1));
        
        return mcm(1, N-1, arr, dp);
    }
};

```

## Complexity Analysis:

### Time Complexity : O(N*N*N)
### Space Complexity: O(N*N) + O(N)


## Tabulation

```Java


class Solution{
public:
    

    int matrixMultiplication(int N, int arr[])
    {
        // code here
        
        vector<vector<int>> dp(N, vector<int> (N, 0));
        
        for(int i=N-1; i>=1; i--) {
            for(int j=i+1; j<=N-1; j++) {
                
                int mini = INT_MAX;
                for(int k=i; k<j; k++){
                    int steps = arr[i-1]*arr[k]*arr[j] + dp[i][k] + dp[k+1][j];
                    mini = min(mini, steps);
                }
                
                dp[i][j] = mini;
            }
        }
        
        return dp[1][N-1];
    }
};


```

## Complexity Analysis:

### Time Complexity : O(N*N*N)
### Space Complexity: O(N*N)