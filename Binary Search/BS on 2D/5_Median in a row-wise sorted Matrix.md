# Median in a row-wise sorted Matrix

[Problem Link](https://www.geeksforgeeks.org/problems/median-in-a-row-wise-sorted-matrix1527/1)

## Approach - 1

1. Change the matrix to 1D array and sort the array and return the middle element

<img width="747" alt="image" src="https://github.com/user-attachments/assets/8e701bc6-f241-4f8a-bb05-ea806354f788">


```Java

public static int median(int matrix[][], int m, int n) {
    List<Integer> lst = new ArrayList<>();

    // Traverse the matrix and
    // copy the elements to the list:
    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {
            lst.add(matrix[i][j]);
        }
    }

    // Sort the list:
    Collections.sort(lst);
    return lst.get((m * n) / 2);
}

```

## Complexity Analysis:

### Time Complexity: O(N \* M) + O((N \* M) \* Log (N \* M))

### Space Complexity: O(N \* M)

## Approach - 2

<img width="745" alt="image" src="https://github.com/user-attachments/assets/34eeb035-ae76-4724-8475-1791b61f189f">

<img width="743" alt="image" src="https://github.com/user-attachments/assets/6c6913e0-7abf-4955-9a33-9e7e17a07e40">


```c++

class Solution{   
public:

    int upperBound(vector<int> &arr, int target) {
        
        int low = 0, high = arr.size();
        
        while(low < high) {
            int mid = (low + high) / 2;
            
            if(arr[mid] <= target) {
                low = mid + 1;
            }
            
            else {
                high = mid;
            }
        }
        
        return low;
    }
    
    int getSmallerElementsCount(vector<vector<int>> &mat, int mid) {
        
        int count = 0;
        
        int n = mat.size();
        int m = mat[0].size();
        
        for(int i=0; i<n; i++) {
            int ele = upperBound(mat[i], mid);
            count += ele;
            //cout<<mid<<" "<<ele<<endl;
        }
        
        return count;
    }

    int median(vector<vector<int>> &mat, int n, int m){
        int low = INT_MAX, high = INT_MIN;
        
        for(int i=0; i<n; i++) {
            low = min(low, mat[i][0]);
            high = max(high, mat[i][m-1]);
        }
        
        int median = (n * m) / 2;
        
        
        while(low <= high) {
            
            int mid = (low + high) / 2;
            
            int smaller = getSmallerElementsCount(mat, mid);
            
            if(smaller <= median) {
                low = mid + 1;   
            }
            
            else {
                high = mid - 1;
            }
        }
        
        return low;
    }
};

```


## Complexity Analysis:

### Time Complexity: O(Log(1e9) * N * Log(M))

### Space Complexity: O(1)

