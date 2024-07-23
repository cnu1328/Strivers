# Ceil The Floor

[Problem Link](https://www.naukri.com/code360/problems/ceiling-in-a-sorted-array_1825401?leftPanelTabValue=PROBLEM)

## Approach - 1

1. Perform upper Bound
2. And check the conditions and return the floor and ciel of the target value

```Java

#include<bits/stdc++.h>

pair<int, int> getFloorAndCeil(vector<int> &a, int n, int target) {
	// Write your code here.
	int index = upper_bound(a.begin(), a.end(), target) - a.begin();

	if(index > 0 && a[index - 1] == target) {
		return {target, target};
	}

	else if(index == 0) {
		return {-1, a[index]};
	}

	else if(index == n) {
		return {a[index-1], -1};
	}

	return {a[index-1], a[index]};
}

```

## Complexity Analysis:

### Time Complexity: O(Log N)

### Space Complexity: O(1)
