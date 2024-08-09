# Nearest Smaller Element

[Problem Link](https://www.interviewbit.com/problems/nearest-smaller-element/)

## Approach - 1

1. Use stack and implement the idea did for previous questions

```c++

vector<int> Solution::prevSmaller(vector<int> &arr) {

    stack<int> st;
    int n = arr.size();
    vector<int> ans(n, -1);

    for(int i=0; i<n; i++) {

        while(!st.empty() && st.top() >= arr[i]) {
            st.pop();
        }

        if(!st.empty()) {
            ans[i] = st.top();
        }

        st.push(arr[i]);
    }

    return ans;

}


```

## Complexity Analysis:

### Time Complexity: O(N + M)

### Space Complexity: (1)
