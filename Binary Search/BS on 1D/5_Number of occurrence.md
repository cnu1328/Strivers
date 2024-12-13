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


## Approach - 2

first find out the upper bound
second find out the lower bound

if both the upper and lower bounds does not point to the target
return 0
else
return the upper - lower + 1

```
class Solution {
    int getLower(int arr[],int n,int x)
    {
        int low = 0 , high = n-1;
        int ans = -1;
        
        while(low <= high)
        {
            int mid = (low+high)/2;
            if(arr[mid] > x)
            {
                high = mid-1;
            }
            else{
                ans = mid;
                low = mid + 1;
            }
        }
        return ans;   
    }
    
    int getCeil(int arr[],int n,int x)
    {
        int low = 0 , high = n-1;
        int ans = -1;
        
        while(low <= high)
        {
            int mid = (low+high)/2;
            if(arr[mid] < x)
            {
                low = mid+1;
            }
            else{
                ans = mid;
                high = mid - 1;
            }
        }
        return ans;
    }
    
    int count(int[] arr, int n, int x) {
        // code here
        
        int c = getCeil(arr,n,x);
        c = c != -1 ? c : 0;
        int f = getLower(arr,n,x);
        f = f != -1 ? f : 0;
        
        if(arr[c] != x && arr[f] != x)
            return 0;
        
        int ans = f-c+1;
        return ans;
    }
```

## Complexity Analysis:

### Time Complexity: O(logn+logn)
### Space Complexity: O(1)

