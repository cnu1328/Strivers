# Partitions With Given Difference

[Problem Link](https://www.codingninjas.com/studio/problems/partitions-with-given-difference_3751628?utm_source=striver&utm_medium=website&utm_campaign=a_zcoursetuf&leftPanelTabValue=PROBLEM)


## Intuition

1. This problem is similar to the DP-17 but with modified target sum.
2. As he given difference, such that s1 - s2 = d.
3. we make s2 = (total - d)/2, so we find total number of ways to make s2 from the given array.
4. We return the answer.

```C++

#include <bits/stdc++.h>


int mod = (int)(1e9 + 7);

int solve(int n, int tar, vector<int> &arr, vector<vector<int>> &dp) {

	if(n == 0) {
		if(tar == 0 && arr[0] == 0) return 2;

		if(tar == 0 || tar == arr[0]) return 1;

		return 0;
	}

	if(dp[n][tar] != -1) return dp[n][tar];

	int notTake = solve(n-1, tar, arr, dp);

	int take = 0;

	if(arr[n] <= tar) take = solve(n-1, tar-arr[n], arr, dp);

	return dp[n][tar] = (notTake + take)%mod;
	
}

int findWays(vector<int>& arr, int k)
{
	int n = arr.size();
	vector<vector<int>> dp(n, vector<int> (k + 1, -1));

	return solve(n-1, k, arr, dp);
}

int countPartitions(int n, int d, vector<int> &arr) {

    int sum = 0;

    for(int num : arr) {
        sum += num;
    }

    if(sum - d < 0 || (sum - d)%2) return false;

    findWays(arr, (sum - d)/2);
}


```

## Complexity Analysis:

### Time Complexity: O(N \* k)

### Space Complexity: O(N \* k) + O(N) (Stack Space)
