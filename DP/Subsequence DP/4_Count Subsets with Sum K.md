# Count Subsets with Sum K

[Problem Link](https://www.codingninjas.com/studio/problems/count-subsets-with-sum-k_3952532?utm_source=striver&utm_medium=website&utm_campaign=a_zcoursetuf)

## Recurssion

1. This problem is Same as Subset sum, where we can return true if subset of elements sum is equal to true otherwise false.
2. Here, If we find the subset Sum then we return 1 else zero.
3. Adding up take and notTake recurrsion call values gives answer.

```Java

import java.util.*;
import java.io.*;

public class Solution {

    int mod = 1000000007;

    public static int findWays(int n, int target, int []nums, int dp[][]) {
        if(target == 0) return 1;

        if(n == 0) {
            if(nums[0] == target) return 1;
            return 0;
        }

        int notTake = findWays(n-1, target, nums, dp);

        int Take = 0;

        if(nums[n] <= target)
            Take = findWays(n-1, target - nums[n], nums, dp);

        return (notTake + Take)%mod;
    }
    public static int findWays(int num[], int tar) {
        int n = num.length;

        return findWays(n-1, tar, num, dp);
    }
}

```

## Complexity Analysis:

### Time complexity: O(2^N)

### Space Complexity: O(N) (stack space)

## Memoization

```C++


int mod = 1e9 + 7;

int solve(int n, int tar, vector<int> &arr, vector<vector<int>> &dp) {

	if(tar == 0) return 1;

	if(n == 0) return (arr[0] == tar);

	if(dp[n][tar] != -1) return dp[n][tar];

	int notTake = solve(n-1, tar, arr, dp);

	int take = 0;

	if(arr[n] <= tar) take =solve(n-1, tar-arr[n], arr, dp);

	return dp[n][tar] = (notTake + take)%mod;
}

int findWays(vector<int>& arr, int k)
{
	int n = arr.size();
	vector<vector<int>> dp(n, vector<int> (k + 1, -1));

	return solve(n-1, k, arr, dp);
}

```

## Complexity Analysis:

### Time Complexity: O(N \* k)

### Space Complexity: O(N \* k) + O(N) (Stack Space)

## Tabulation

```Java


int mod = 1e9 + 7;


int findWays(vector<int>& arr, int k)
{
	int n = arr.size();
	vector<vector<long>> dp(n, vector<long> (k + 1, 0));

	for(int i=0; i<n; i++) {
		dp[i][0] = 1;
	}

	if(arr[0] <= k) dp[0][arr[0]] = 1;

	for(int i=1; i<n; i++) {
		for(int j=1; j<=k; j++) {
			long notTake = dp[i-1][j];

			long take = 0;

			if(arr[i] <= j) {
				take = dp[i-1][j-arr[i]];
			}

			dp[i][j] = (take + notTake)%mod;
		}
	}

	return (int)dp[n-1][k];

	// return solve(n-1, k, arr, dp);
}


```

## Complexity Analysis:

### Time Complexity: O(N \* k)

### Space Complexity: O(N \* k)

## Space Optimization

```C++


int mod = 1e9 + 7;

int findWays(vector<int>& arr, int k)
{
	int n = arr.size();
	vector<int> dp(k+1, 0), curr(k+1);
	dp[0] = curr[0] = 1;
	if(arr[0] <= k) dp[arr[0]] = 1;

	for(int i=1; i<n; i++) {
		for(int j=1; j<=k; j++) {
			long notTake = dp[j];

			long take = 0;

			if(arr[i] <= j) {
				take = dp[j-arr[i]];
			}

			curr[j] = (take + notTake)%mod;
		}
		dp = curr;
	}

	return (int)dp[k];

	// return solve(n-1, k, arr, dp);
}

```

## Complexity Analysis:

### Time Complexity: O(N \* k)

### Space Complexity: O(N)

## What if the array values include 0's. The answer might be wrong.

1. suppose the array => {0, 0, 1} the answer is 4. but with the help of above code we get 1.
2. This is because of if(sum == 0) return 1;
3. Now we are trying to modify this sum == 0 condition

```C++


int mod = 1e9 + 7;

int solve(int n, int tar, vector<int> &arr, vector<vector<int>> &dp) {



	if(n == 0) {
		if(tar == 0 && arr[0] == 0) return 2;

		if(tar == 0 || tar == arr[0]) return 1;

		return 0;
	}

	if(dp[n][tar] != -1) return dp[n][tar];

	int notTake = solve(n-1, tar, arr, dp);

	int take = 0;

	if(arr[n] <= tar) take =solve(n-1, tar-arr[n], arr, dp);

	return dp[n][tar] = (notTake + take)%mod;
}

int findWays(vector<int>& arr, int k)
{
	int n = arr.size();
	vector<vector<int>> dp(n, vector<int> (k + 1, -1));

	return solve(n-1, k, arr, dp);
}

```

## Complexity Analysis:

### Time Complexity: O(N \* k)

### Space Complexity: O(N \* k) + O(N) (Stack Space)
