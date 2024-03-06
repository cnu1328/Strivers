# Rod cutting problem

[Problem Link](https://www.codingninjas.com/studio/problems/rod-cutting-problem_800284?utm_source=striver&utm_medium=website&utm_campaign=a_zcoursetuf&leftPanelTabValue=PROBLEM)

## Recurrsion

1. This approach is same as unbounded Knapsack, but here the n itself is weight and its indexes

```Java

public class Solution {
	static int solve(int n, int w, int price[]) {
		if(w == 0) return 0;

		if(n == 1) {
			if(w%n == 0) return (w/n)*price[0];
			return 0;
		}

		int notTake = solve(n-1, w, price);
		int take = 0;

		if(n <= w) {
			take = price[n-1] + solve(n, w - n, price);
		}
		return Math.max(notTake, take);
	}
	public static int cutRod(int price[], int n) {
		return solve(n, n, price);
	}
}

```

## Complexity Analysis:

### Time Complexity: O(2^N)

### Space Complexity: O(N) (Stack Space)

## Memoization

```Java

public class Solution {
	static int solve(int n, int w, int price[], int dp[][]) {
		if(w == 0) return 0;

		if(n == 1) {
			if(w%n == 0) return (w/n)*price[0];
			return 0;
		}

		if(dp[n-1][w] != -1) return dp[n-1][w];

		int notTake = solve(n-1, w, price, dp);
		int take = 0;

		if(n <= w) {
			take = price[n-1] + solve(n, w - n, price, dp);
		}
		return dp[n-1][w] = Math.max(notTake, take);
	}
	public static int cutRod(int price[], int n) {
		int dp[][] = new int[n][n+1];

		for(int i=0; i<n; i++) {
			for(int j=0; j<=n; j++) {
				dp[i][j] = -1;
			}
		}
		return solve(n, n, price, dp);
	}
}

```

## Complexity Analysis:

### Time Complexity: O(N*N)

### Space Complexity: O(N*N) + O(N) (Stack Space)