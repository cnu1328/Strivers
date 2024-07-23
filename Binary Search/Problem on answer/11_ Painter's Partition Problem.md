# Painter's Partition Problem

[Problem Link](https://www.naukri.com/code360/problems/painter-s-partition-problem_1089557)

## Approach - 1 - Brute Force Approach

1. It is same as the approach we did in the allocate books

## Approach - 2 - Using Binary Search

2. It is same as the approach we didi in the allocate books

```Java

#include<bits/stdc++.h>
int findPainters(vector<int> boards, int units) {
    int numOfBorads = 1, sumOfUnits = 0;

    for(int i=0; i<boards.size(); i++) {
        if(sumOfUnits + boards[i] <= units) {
            sumOfUnits += boards[i];
        }

        else {
            sumOfUnits = boards[i];
            numOfBorads++;
        }
    }

    return numOfBorads;
}

int findLargestMinDistance(vector<int> &boards, int k)
{
   int low = *max_element(boards.begin(), boards.end());
   int high = accumulate(boards.begin(), boards.end(), 0);

   int mini = INT_MAX;

   while(low <= high) {
       int mid = (low + high) >> 1;

       int Tpainters = findPainters(boards, mid);

       if(Tpainters <= k) {
           mini = min(mini, mid);
           high = mid - 1;
       } else {
           low = mid + 1;
       }
   }

   return mini;
}

```

## Complexity Analysis:

### Time Complexity: O(N \* Log X) where X = [max(arr), sum(arr)]

### Space Complexity: O(1)
