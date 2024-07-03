# Perfect Sum Problem

[Problem Link](https://www.geeksforgeeks.org/problems/perfect-sum-problem5633/1)


## Approach - Recurssion

1. implement take and not take case, while you are taking an element then decrement sum by the element other wise not
2. return the sum of take and notTake

```Java

class Solution{
    
    private int sos(int index, int arr[], int sum) {
        
        if(sum < 0) return 0;
        
        if(index < 0) {
            if(sum == 0) return 1;
            return 0;
        }
        
        int take = 0, notTake = 0;
        
        take = sos(index -1, arr, sum - arr[index]);
        notTake = sos(index - 1, arr, sum);
        
        return (take + notTake);
        
        
    }

	public int perfectSum(int arr[],int n, int sum) 
	{ 
	    return sos(n-1, arr, sum);
	} 
}

```

## Complexity Analysis:

### Time Complexity: O(2^N) 

### Space Complexity: O(N)


## Approach - Memoization - Top Down Approach

```Java

class Solution{
    
    int mod = 1_000_000_000 + 7;
    
    private int sos(int index, int arr[], int sum, int dp[][]) {
        
        if(sum < 0) return 0;
        
        if(index == 0) {
            if(sum == 0) return 1;
            return 0;
        }
        
        if(dp[index][sum] != -1) return dp[index][sum];
        
        int take = 0, notTake = 0;
        
        take = sos(index - 1, arr, sum - arr[index-1], dp)%mod;
        notTake = sos(index - 1, arr, sum, dp)%mod;
        
        return dp[index][sum] = (take + notTake)%mod;
        
        
    }

	public int perfectSum(int arr[],int n, int sum) 
	{ 
	    int dp[][] = new int[n+1][sum+1];
	    
	    for(int i=0; i<=n; i++) {
	        Arrays.fill(dp[i], -1);
	    }
	    
	    return sos(n, arr, sum, dp)%mod;
	} 
}

```

## Complexity Analysis:

### Time Complexity: O(N*Sum) 

### Space Complexity: O(N*Sum) + O(N)

## Tabulation - Bottom Up Approach

```Java

class Solution{
    
    int mod = 1_000_000_000 + 7;

	public int perfectSum(int arr[],int n, int sum) 
	{ 
	    int dp[][] = new int[n+1][sum+1];
	    
	    dp[0][0]  = 1;
	    
	    for(int i=1; i<=n; i++) {
	        for(int j=0; j<=sum; j++) {
	            
	            
	            int take = 0, notTake = 0;
	           
	            if(arr[i-1] <= j) {
	                take = dp[i-1][j-arr[i-1]]%mod;
	            }
	            
	            notTake = dp[i-1][j]%mod;
	            
	            dp[i][j] = (take + notTake)%mod;
	        }
	    }
	    
	    return dp[n][sum]%mod;
	} 
}

```

## Complexity Analysis:

### Time Complexity: O(N*Sum) 

### Space Complexity: O(N*Sum) 
