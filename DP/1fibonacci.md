# Fibonacci Series

[Problem Link](https://www.codingninjas.com/studio/problems/nth-fibonacci-number_74156?utm_source=striver&utm_medium=website&utm_campaign=a_zcoursetuf&leftPanelTabValue=PROBLEM)

## Intuition

1. As we calculate, the fibonacci with the help of f(n) = f(n-1) + f(n-2)
2. But, This lead to TLE, so its better to go with memoization(Top-Down Dp)
3. We also solve this same question with the help of Tabulation(Bottom-up Dp)
4. And next, we solve this question with the help of space optimization that is O(1)

## Code

## Recurssion

```Java


import java.util.*;
public class Solution {


	static int findFibo(int num, int[] dp) {
		if(num <= 1) return num;

		return findFibo(num-1, dp) + findFibo(num-2, dp);
	}

	public static void main(String[] args) {

		Scanner sc = new Scanner(System.in);
		int n = sc.nextInt();

		int[] dp = new int[n+1];

		for(int i=0; i<=n; i++) {
			dp[i] = -1;
		}

		System.out.println(findFibo(n, dp));

	}

}

```

## Complexity Analysis

### Time Complexity: O(exponential)

### Space Complexity: O(stack space)

## Memoization

```Java

import java.util.*;
public class Solution {


	static int findFibo(int num, int[] dp) {
		if(num <= 1) return num;

		if(dp[num] != -1) return dp[num];
		return dp[num] = findFibo(num-1, dp) + findFibo(num-2, dp);
	}

	public static void main(String[] args) {

		Scanner sc = new Scanner(System.in);
		int n = sc.nextInt();

		int[] dp = new int[n+1];

		for(int i=0; i<=n; i++) {
			dp[i] = -1;
		}

		System.out.println(findFibo(n, dp));

	}

}

```

## Complexity Analysis

### Time Complexity: O(N)

### Space Complexity: O(N) + O(Stack space)

## Tabulation(Bottom - up) => Base case to Required answer

```Java

import java.util.*;
public class Solution {

	public static void main(String[] args) {
		
		Scanner sc = new Scanner(System.in);
		int n = sc.nextInt();

		int[] dp = new int[n+1];
		dp[0] = 0;
		dp[1] = 1;

		for(int i=2; i<=n; i++) {
			dp[i] = dp[i-1] + dp[i-2];
		}

		System.out.println(dp[n]);
		
	}

}


```

## Complexity Analysis

### Time Complexity: O(N)

### Space Complexity: O(N)



## Space Optimization

```Java

import java.util.*;
public class Solution {

	public static void main(String[] args) {
		
		Scanner sc = new Scanner(System.in);
		int n = sc.nextInt();

		int prev2 = 0, prev = 1;

		for(int i=2; i<=n; i++) {
			int curr = prev + prev2;
			prev2 = prev;
			prev = curr;
		}

		System.out.println(prev);
		
	}

}
```

## Complexity Analysis

### Time Complexity: O(N)

### Space Complexity: O(1)