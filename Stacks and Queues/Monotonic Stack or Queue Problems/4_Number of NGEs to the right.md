# Number of NGEs to the right

[Problem Link](https://www.geeksforgeeks.org/problems/number-of-nges-to-the-right/1)

## Approach - 1 - Brute Force Approach

1. First find the number of next Greater elements to the right for a given number
2. Traverse the queries and find the answers respective to the given indices

```c++

class Solution{
public:

    vector<int> count_NGE(int n, vector<int> &arr, int queries, vector<int> &indices){
        //write your code here\

        vector<int> next(n, 0);

        for(int i=0; i<n; i++) {
            for(int j=i+1; j<n; j++) {
                if(arr[j] > arr[i]) {
                    next[i]++;
                }
            }
        }

        vector<int> ans;

        for(int i=0; i<queries; i++) {
            ans.push_back(next[indices[i]]);
        }

        return ans;

    }

};

```

## Complexity Analysis:

### Time Complexity: O(N ^ 2) (TLE)

### Space Complexity: (1)

## Approach - 2

1. For every index in the query, find the number of Next greater elements from index to N in the given array

```c++

class Solution{
public:

    vector<int> count_NGE(int n, vector<int> &arr, int queries, vector<int> &indices){
        //write your code here\

        vector<int> ans;

        for(int i=0; i<queries; i++) {
            int index = indices[i];
            int count = 0;
            for(int j = index + 1; j < n; j++) {
                if(arr[j] > arr[index]) {
                    count++;
                }
            }

            ans.push_back(count);
        }

        return ans;

    }

};

```

## Complexity Analysis:

### Time Complexity: O(N \* queries)

### Space Complexity: (1)

## Approach - 3 - Stack based approach

```c++

class Solution{
public:

    vector<int> count_NGE(int n, vector<int> &arr, int q, vector<int> &indices){
        //write your code here
        vector<int> ans(q);
        for (int i = 0; i < q; i++) {
            int curr = arr[indices[i]];
            stack<int> st;
            int r = n - 1;
            while (r > indices[i]) {
                if (arr[r] > curr) {
                    st.push(arr[r]);
                }
                r--;
            }
            ans[i] = st.size();
        }
        return ans;
       
    }

};

```
