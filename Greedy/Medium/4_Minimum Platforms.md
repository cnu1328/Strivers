# Minimum Platforms

[Problem Link](https://www.geeksforgeeks.org/problems/minimum-platforms-1587115620/1)

## Approach - 1

1. First sort the given arrival times and depature times, to know when a train arraivals and depature of any train
2. If arrival of any train is less than or equal to the depature of any train, in this case we require other platform.
3. In above case we increment the platform by 1 and will move right pointer to the next arrival train, to know during this train any train arrived
4. In other case, a train arrived, by the time no train is in the platform, in this we can decrease the platform by 1 and move left pointer to next depature of the train

```c++

class Solution{
    public:

    int findPlatform(int arr[], int dep[], int n)
    {
    	sort(arr, arr+n);
    	sort(dep, dep+n);

    	int platform = 1;
    	int ans = 1;

    	int left = 0, right = 1;

    	while(right < n && left < n) {

    	    if(arr[right] <= dep[left]) {
    	        platform++;
    	        right++;
    	    } else {
    	        platform--;
    	        left++;
    	    }

    	    ans = max(ans, platform);
    	}

    	return ans;
    }
};

```

## Complexity Analysis:

### Time Complexity: O(N Log N + (M + N))

### Space Complexity: (1)
