# K-th element of two Arrays

[Problem Link](https://www.geeksforgeeks.org/problems/k-th-element-of-two-sorted-array1317/1)

## Approach - 1 - Brute Force

1. Use two pointers one points to first array and other one points to second array
2. use while loop to sort for every i, j the check the which one is smaller and which one is bigger
3. based on that write conditions
4. At any point of time, if count becomes equal to K then return the index

```Java

class Solution{
    public:
    int kthElement(int arr1[], int arr2[], int n, int m, int k)
    {
        int i = 0, j = 0;

        int count = 0;

        while(i < n && j < m) {
            if(arr1[i] <= arr2[j]) {
                count++;
                if(count == k)
                    return arr1[i];
                i++;
            }

            else {

                count++;
                if(count == k)
                    return arr2[j];
                j++;
            }

        }

        while(i < n) {

            count++;
            if(count == k)
                    return arr1[i];
            i++;
        }

        while(j < m) {

            count++;
            if(count == k)
                return arr2[j];
            j++;
        }
    }
};

```

## Complexity Analysis:

### Time Complexity: O(N + M)

### Space Complexity: O(1)

## Approach - 2 - Binary Search

```c++

class Solution {
  public:
    int kthElement(int k, vector<int>& nums1, vector<int>& nums2) {
        
        int n = nums1.size();
        int m = nums2.size();
        
        if(n > m) return kthElement(k, nums2, nums1);
        
        // k - m (big size array)
        int low = max(0, k - m); // Try to maximize the low, because of our leftHalf
        
        // 
        int high = min(k, n); // Try to minizie the high, because of leftHalf
        
        int leftHalf = k;
        
        while(low <= high) {
            

            int mid1 = (low + high) / 2;
            int mid2 = leftHalf - mid1;
            
            int l1, l2, r1, r2;
            
            l1 = l2 = INT_MIN;
            r1 = r2 = INT_MAX;
            
            if(mid1 < n) r1 = nums1[mid1];
            
            if(mid2 < m) r2 = nums2[mid2];
            
            if(mid1 > 0) l1 = nums1[mid1 - 1];
            
            if(mid2 > 0) l2 = nums2[mid2 - 1];
            
            
            
            if(l1 <= r2 && l2 <= r1) {
                return max(l1, l2);
            }
            
            if(l1 > r2) {
                high = mid1 - 1;
            }
            
            else {
                low = mid1 + 1;
            }
        }
        
        return 0;
    }
};

```

## Complexity Analysis:

### Time Complexity: O(Log(min(N, M)))

### Space Complexity: O(1)
