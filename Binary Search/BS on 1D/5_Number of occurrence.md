# Number of occurrence

[Problem Link](https://www.geeksforgeeks.org/problems/number-of-occurrence2259/1)

## Approach - 1

1. Linear Search and count the occurences

```Java

class Solution{
public:

	int count(int arr[], int n, int x) {
	    int cnt = 0;

	    for(int i=0; i<n; i++) {
	        if(arr[i] == x) cnt++;
	    }
	    return cnt;
	}
};

```

## Complexity Analysis:

### Time Complexity: O(N)

### Space Complexity: O(1)
