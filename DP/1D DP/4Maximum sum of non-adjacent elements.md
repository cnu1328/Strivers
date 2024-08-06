# Maximum sum of non-adjacent elements

[Problem Link(codestudio)](https://www.codingninjas.com/studio/problems/maximum-sum-of-non-adjacent-elements_843261?utm_source=striver&utm_medium=website&utm_campaign=a_zcoursetuf&leftPanelTabValue=PROBLEM)

[Problem Link(Leetcode)](https://leetcode.com/problems/house-robber/)

## Approach(Recurssion)

1. use the concept of pick and not pick
2. While you are pick the element, add its index array value to pick and call recurssion by decreasing its index by 2(non-adjacent)
3. while not picking, just call the function by decreasing its index by 1
4. return maximum of pick and not pick

```Java

public class Solution {

	public static int maximumSum(int ind, ArrayList<Integer> nums) {

		if(ind == 0) return nums.get(ind);

		if(ind < 0) return 0;

		int pick = nums.get(ind) + maximumSum(ind-2, nums);
		int notpick = maximumSum(ind-1, nums);

		return Math.max(pick, notpick);
	}
	public static int maximumNonAdjacentSum(ArrayList<Integer> nums) {
		return maximumSum(nums.size() - 1,f nums);
	}
}
```

## Complexity Analysis

### Time Complexity: O(2^N)

### Space Complexity: O(stack Space)

## Memoization

1. Use dp array, to reduce the time limit from exponential to O(N)
2. Initialize dp with -1

```Java

public class Solution {

	public static int maximumSum(int ind, ArrayList<Integer> nums, int dp[]) {

		if(ind == 0) return nums.get(ind);

		if(ind < 0) return 0;

		if(dp[ind] != -1) return dp[ind];

		int pick = nums.get(ind) + maximumSum(ind-2, nums, dp);
		int notpick = maximumSum(ind-1, nums, dp);

		return dp[ind] = Math.max(pick, notpick);
	}
	public static int maximumNonAdjacentSum(ArrayList<Integer> nums) {
		int n = nums.size();
		int dp[] = new int[n];

		for(int i=0; i<n; i++) {
			dp[i] = -1;
		}
		return maximumSum(n - 1, nums, dp);
	}
}
```

## Complexity Analysis

### Time Complexity: O(N)

### Space Complexity: O(N) + O(N) stack space

## Tabulation

1. Anaylze the memoization code, and write base cases and analyze pattern

```Java

public class Solution {
	public static int maximumNonAdjacentSum(ArrayList<Integer> nums) {
		int n = nums.size();
		int dp[] = new int[n];

		dp[0] = nums.get(0);

		for(int i=1; i<n; i++) {

			int take = nums.get(i) + (i > 1 ? dp[i-2] : 0);
			int nottake = dp[i-1];

			dp[i] = Math.max(take, nottake);
		}

		return dp[n-1];
	}
}
```

## Complexity Analysis

### Time Complexity: O(N)

### Space Complexity: O(N)

## Space Optimization

1. See the pattern, i-2 and i-1 for i

```Java

public class Solution {
	public static int maximumNonAdjacentSum(ArrayList<Integer> nums) {
		int n = nums.size();
		int prev = nums.get(0);
		int prev2 = 0;

		for(int i=1; i<n; i++) {

			int take = nums.get(i);

			if(i > 1) take += prev2;

			int nottake = prev;

			int curr = Math.max(take, nottake);
			prev2 = prev;
			prev = curr;
		}

		return prev;
	}
}

```

## Complexity Analysis

### Time Complexity: O(N)

### Space Complexity: O(1)
