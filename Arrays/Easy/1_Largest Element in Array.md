# Largest Element in Array

[Problem Link](https://www.geeksforgeeks.org/problems/largest-element-in-array4009/0)

## Approach - 1

1. Traverse the given array, and compare the current element with the maximum element
2. If current element greater than maximum then asign maximum element with current element

```Java

class Solution
{
public:
    int largest(vector<int> &arr, int n)
    {
        int max=0;
        for(int i=0;i<n;i++){
            if(max<arr[i])
                max = arr[i];
        }

        return max;
    }
};

```

## Complexity Analysis:

### Time Complexity: O(N)

### Space Complexity: O(1)

## Approach - 2

1. We also solve this question with the help of sorting the given array in ascending order and returning the last element(n-1 the) element

## Complexity Analysis:

### Time Complexity: O(N Log n)

### Space Complexity: O(1)
