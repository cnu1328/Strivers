# Shortest Job first

[Problem LInk](https://www.geeksforgeeks.org/problems/shortest-job-first/1)

## Approach - 1

1. sort the given array
2. Traverse the array and completion time and weight time
3. return the average weight time

```c++

class Solution {
  public:
    long long solve(vector<int>& bt) {
        long long ans = 0;
        int n = bt.size();

        sort(bt.begin(), bt.end());
        long long ct = 0;
        long long wt = 0;

        for(int i=0; i<n; i++) {
            ct += bt[i];

            wt += (ct - bt[i]);

        }

        return (wt / (long long)n);
    }
};

```

## Complexity Analysis:

### Time Complexity: O(N Log N)

### Space Complexity: (1)
