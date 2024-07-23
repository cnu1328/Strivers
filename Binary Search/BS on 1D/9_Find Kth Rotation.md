# Find Kth Rotation

[Problem Link](https://www.geeksforgeeks.org/problems/rotation4723/1)

## Approach - 1

1. It is similar to finding the minimum element, as we did in the previous problem,
2. A small change is that, we need to find the index of minimum element of the given array
3. One Obeservation is that, if nums[low] <= nums[high], it means the entire sub-array is sorted, so we can know he `nums[low]` is minimum element. Find the minimum from that and respective index
4. And do binary search, we can solve this problem

```Java

//User function template for C++
class Solution{
public:
	int findKRotation(int arr[], int n) {
	    int low = 0, high = n-1;
	    int mini = INT_MAX;
	    int index = -1;

	    while(low <= high) {
	        int mid = (low + high)/2;

	        if(arr[low] <= arr[high]) {
	            if(arr[low] < mini) {
	                mini = arr[low];
	                index = low;
	            }

	            break;
	        }

	        if(arr[low] <= arr[mid]) {
	            if(arr[low] < mini) {
	                mini = arr[low];
	                index = low;
	            }
	            low = mid + 1;
	        }

	        else {
	            if(arr[mid] < mini) {
	                mini = arr[mid];
	                index = mid;
	            }
	            high = mid - 1;
	        }
	    }

	    return index;
	}

};

```

## Complexity Analysis:

### Time Complexity: O(Log N)

### Space Complexity: O(1)
