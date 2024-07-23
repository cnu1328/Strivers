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

## Approach - 2
