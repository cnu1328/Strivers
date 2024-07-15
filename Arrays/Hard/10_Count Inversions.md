# Count Inversions

[Problem Link](https://www.geeksforgeeks.org/problems/inversion-of-array-1587115620/1)

## Approach - 1

1. Use two loops and check whether arr[i] > arr[j], then incrmeent the answer

```Java

class Solution {
    // arr[]: Input Array
    // N : Size of the Array arr[]
    // Function to count inversions in the array.
    static long inversionCount(long arr[], int n) {
        // Your Code Here

        long ans = 0;

        for(int i=0; i<n; i++) {

            for(int j=i+1; j<n; j++) {
                if(arr[i] > arr[j]) ans++;
            }
        }

        return ans;
    }
}
```

## Complexity Analysis:

### Time Complexity: O(N)

### Space Complexity: O(1)

## Approach - 2 - Using Merge Sort

```Java

class Solution {

    static long merge(long arr[], int start, int mid, int end) {
        int n = arr.length;

        ArrayList<Long> temp = new ArrayList<>();
        long count = 0;

        int left = start, right = mid + 1, k = 0;

        while(left <= mid && right <= end) {
            if(arr[left] <= arr[right]) {
                temp.add(arr[left++]);
            }

            else {
                count += (mid - left + 1);
                temp.add(arr[right++]);
            }
        }

        while(left <= mid) {
            temp.add(arr[left++]);
        }

        while(right <= end) {
            temp.add(arr[right++]);
        }

        for(int i = start; i<=end; i++) {
            arr[i] = temp.get(i - start);
        }

        return count;
    }

    static long mergeSort(long arr[], int start, int end) {
        long count = 0L;
        if(start < end) {
            int mid = (start + end)/2;

            count += mergeSort(arr, start, mid);
            count += mergeSort(arr, mid + 1, end);
            count += merge(arr, start, mid, end);
        }

        return count;
    }
    // arr[]: Input Array
    // N : Size of the Array arr[]
    // Function to count inversions in the array.
    static long inversionCount(long arr[], int n) {
        // Your Code Here

        return mergeSort(arr, 0, n-1);
    }
}

```

## Complexity Analysis:

### Time Complexity: O(N Log N)

### Space Complexity: O(N)
