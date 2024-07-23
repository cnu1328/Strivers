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
