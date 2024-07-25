# Median in a row-wise sorted Matrix

[Problem Link](https://www.geeksforgeeks.org/problems/median-in-a-row-wise-sorted-matrix1527/1)

## Approach - 1

1. Change the matrix to 1D array and sort the array and return the middle element

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
