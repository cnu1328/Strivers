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


#include <bits/stdc++.h>
using namespace std;

int kthElement(vector<int> &a, vector<int>& b, int m, int n, int k) {
    if (m > n) return kthElement(b, a, n, m, k);

    int left = k; //length of left half

    //apply binary search:
    int low = max(0, k - n), high = min(k, m);
    while (low <= high) {
        int mid1 = (low + high) >> 1;
        int mid2 = left - mid1;
        //calculate l1, l2, r1 and r2;
        int l1 = INT_MIN, l2 = INT_MIN;
        int r1 = INT_MAX, r2 = INT_MAX;
        if (mid1 < m) r1 = a[mid1];
        if (mid2 < n) r2 = b[mid2];
        if (mid1 - 1 >= 0) l1 = a[mid1 - 1];
        if (mid2 - 1 >= 0) l2 = b[mid2 - 1];

        if (l1 <= r2 && l2 <= r1) {
            return max(l1, l2);
        }

        //eliminate the halves:
        else if (l1 > r2) high = mid1 - 1;
        else low = mid1 + 1;
    }
    return 0; //dummy statement

}

int main()
{
    vector<int> a = {2, 3, 6, 7, 9};
    vector<int> b = {1, 4, 8, 10};
    cout << "The k-th element of two sorted array is: " <<
            kthElement(a, b, a.size(), b.size(), 5) << '\n';
}
        


```

## Complexity Analysis:

### Time Complexity: O(Log(min(N, M)))

### Space Complexity: O(1)
