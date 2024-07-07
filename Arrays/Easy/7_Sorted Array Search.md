# Sorted Array Search

[Problem Link](https://www.geeksforgeeks.org/problems/who-will-win-1587115621/1)

## Approach - 1 - Linear Search

1. Traverse the entire array and check if given element exist in it or not
2. if exists return true or flase

## Complexity Analysis:

### Time Complexity: O(N)

### Space Complexity: O(1)

## Approach - 2 - Binary Search - Iterative

1. Try to reduce the search space for every iteration
2. Use binary search algorithm
   - For two indices, calculate the middile index => `mid = start + (end - start)/2`
   - Check if the search element is greater than `nums[mid]` then reduce the search space by left side
   - or else reduce search space by right
   - if `nums[mid]` === search element then return true

```Java

class Solution{
    public:

    int searchInSorted(int arr[], int N, int K)
    {
        int f,l,mid;
        low=0;
        high= N-1;

        while(low <= high){

            mid = (low + high)/2;

            if(arr[mid]<K){
                low = mid+1;
            }
            else if(arr[mid]==K){
                return 1;
            }
            else
                high = mid-1;
        }

        return -1;
    }
};

```

## Complexity Analysis:

### Time Complexity: O(log N)

### Space Complexity: O(1)

## Approach - Binary Search - Recurssion

```Java

class Solution{
    public:

    int binary(int arr[],int f,int l,int k){
        int mid;
        if(f<=l){
            mid = (f+l)/2;
            if(arr[mid]<k)
                return binary(arr,mid+1,l,k);
            else if(arr[mid]==k)
                return 1;
            return binary(arr,f,mid-1,k);
        }
        return -1;
    }

    int searchInSorted(int arr[], int N, int K)
    {
        int f,l,mid;
        f=0;
        l= N-1;
        return binary(arr,f,l,K);
    }
};


```

## Complexity Analysis:

### Time Complexity: O(log N)

### Space Complexity: O(1)
