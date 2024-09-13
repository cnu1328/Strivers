# Row with max 1s

[Problem Link](https://www.geeksforgeeks.org/problems/row-with-max-1s0023/1)

## Approach - 1 - Brute Force Approach

1. Traverse the matrix, for every row sum each cell
2. If you find a row with maximum sum, then update answer Index
3. return the answer Index

```Java

class Solution{
public:
	int rowWithMax1s(vector<vector<int> > arr, int n, int m) {
	    // code here
	    int indx = -1, cnt = 0;

	    for(int i=0; i<n; i++) {
	        int count = 0;
	        for(int j=m-1; j>=0; j--) {
	            if(arr[i][j] == 1) {
	                count++;
	            }
	            else
	                break;
	        }

	        if(cnt < count) {
	            cnt = count;
	            indx = i;
	        }
	    }

	    return indx;
	}

};

```

## Complexity Analysis:

### Time Complexity: O(N \* M)

### Space Complexity: O(1)

## Approach - 2 - Binary Search

1. Use lower bound, to find the first position of `1` in the row => lower_bound(1) as `ind`
2. Use upper bound, to find the first position of `1` in the row => upper_bound(0)
3. The number of ones in a row can be obtained m - ind
4. Find the maximum one's index out of all

```Java

class Solution {

    private int lowerBound(int arr[], int m, int target) {
        int low = 0, high = m - 1;

        while(low < high) {
            int mid = low + (high - low)/2;

            if(arr[mid] >= 1) {
                high = mid;
            } else {
                low = mid + 1;
            }
        }

        return low;
    }

    public int rowWithMax1s(int arr[][]) {

        int index = -1, maxi = 0;

        int n = arr.length;
        int m = arr[0].length;

        for(int i=0; i<n; i++) {

            int count = m - lowerBound(arr[i], m, 1);

            if(count > maxi) {
                maxi = count;
                index = i;
            }
        }

        return index;
    }
}

```

## Complexity Analysis:

### Time Complexity: O(N \* Log M)

### Space Complexity: O(1)
