# Cherry PickUp II

[Problem Link](https://leetcode.com/problems/cherry-pickup-ii/)

## Recurssion

### Code

```Java

import java.util.* ;
import java.io.*;
public class Solution {

	static int helper(int i, int j1, int j2, int r, int c, int[][] grid) {

		if(j1 < 0 || j1 >= c || j2 < 0 || j2 >= c) return -1000000000;

		if(i == r-1) {
			if(j1 == j2) return grid[i][j1];

			return (grid[i][j1] + grid[i][j2]);
		}

		int maxi = 0;

		for(int da = -1; da<2; da++) {
			for(int db = -1; db < 2; db++) {
				if(j1 == j2) {
					maxi = Math.max(maxi, grid[i][j1] +  helper(i+1, j1+da, j2+db, r, c, grid));
				} else {
					maxi = Math.max(maxi, grid[i][j1] + grid[i][j2] + helper(i+1, j1+da, j2+db, r, c, grid));
				}
			}
		}

		return maxi;
	}

	public static int maximumChocolates(int r, int c, int[][] grid) {

		return helper(0, 0, c-1, r, c, grid);
	}
}


```

## Complexity Analysis

### Time Complexity: O(3^N \* 3^N);

### Space Complexity: O(N)

## Memoization

```Java

import java.util.* ;
import java.io.*;
public class Solution {

	static int helper(int i, int j1, int j2, int r, int c, int[][] grid, int[][][] dp) {

		if(j1 < 0 || j1 >= c || j2 < 0 || j2 >= c) return -1000000000;

		if(i == r-1) {
			if(j1 == j2) return grid[i][j1];

			return (grid[i][j1] + grid[i][j2]);
		}

		if(dp[i][j1][j2] != -1) return dp[i][j1][j2];

		int maxi = 0;

		for(int da = -1; da<2; da++) {
			for(int db = -1; db < 2; db++) {
				if(j1 == j2) {
					maxi = Math.max(maxi, grid[i][j1] +  helper(i+1, j1+da, j2+db, r, c, grid, dp));
				} else {
					maxi = Math.max(maxi, grid[i][j1] + grid[i][j2] + helper(i+1, j1+da, j2+db, r, c, grid, dp));
				}
			}
		}

		return dp[i][j1][j2] = maxi;
	}

	public static int maximumChocolates(int r, int c, int[][] grid) {

		int dp[][][] = new int[r][c][c];

		for(int i=0; i<r; i++) {
			for(int j=0; j<c; j++) {
				for(int k=0; k<c; k++) {
					dp[i][j][k] = -1;
				}
			}
		}
		return helper(0, 0, c-1, r, c, grid, dp);
	}
}

```

## Complexity Analysis

### Time Complexity: O(N*M*M);

### Space Complexity: O(N*M*M) + O(N)

## Tabulation

```Java


import java.util.* ;
import java.io.*;
public class Solution {



	public static int maximumChocolates(int r, int c, int[][] grid) {

		int dp[][][] = new int[r][c][c];

		for(int i=0; i<c; i++) {
			for(int j=0; j<c; j++) {
				if(i == j) dp[r-1][i][j] = grid[r-1][j];

				else dp[r-1][i][j] = grid[r-1][i] + grid[r-1][j];
			}
		}

		for(int i=r-2; i>=0; i--) {
			for(int j1 = 0; j1<c; j1++) {
				for(int j2=0; j2<c; j2++) {

					int maxi = 0;

					for(int da = -1; da<2; da++) {
						for(int db = -1; db < 2; db++) {
							int value = 0;

							if(j1 == j2) value += grid[i][j1];

							else value += grid[i][j1] + grid[i][j2];

							if(j1 + da >= 0 && j1 + da < c && j2 + db >= 0 && j2 + db < c)
								value += dp[i+1][j1+da][j2+db];

							else {
								value += -1000000000;
							}

							maxi = Math.max(maxi, value);
						}
					}

					dp[i][j1][j2] = maxi;
				}
			}
		}

		return dp[0][0][c-1];
	}
}

```

## Complexity Analysis

### Time Complexity: O(N*M*M);

### Space Complexity: O(N*M*M)

## Space Optimization

```Java

import java.util.* ;
import java.io.*;
public class Solution {



	public static int maximumChocolates(int r, int c, int[][] grid) {

		int front[][] = new int[c][c];

		for(int i=0; i<c; i++) {
			for(int j=0; j<c; j++) {
				if(i == j) front[i][j] = grid[r-1][j];

				else front[i][j] = grid[r-1][i] + grid[r-1][j];
			}
		}

		for(int i=r-2; i>=0; i--) {

			int curr[][] = new int[c][c];
			for(int j1 = 0; j1<c; j1++) {
				for(int j2=0; j2<c; j2++) {

					int maxi = 0;

					for(int da = -1; da<2; da++) {
						for(int db = -1; db < 2; db++) {
							int value = 0;

							if(j1 == j2) value += grid[i][j1];

							else value += grid[i][j1] + grid[i][j2];

							if(j1 + da >= 0 && j1 + da < c && j2 + db >= 0 && j2 + db < c)
								value += front[j1+da][j2+db];

							else {
								value += -1000000000;
							}

							maxi = Math.max(maxi, value);
						}
					}

					curr[j1][j2] = maxi;
				}
			}

			front = curr;
		}

		return front[0][c-1];
	}
}

```

## Complexity Analysis

### Time Complexity: O(N*M*M);

### Space Complexity: O(M*M)
