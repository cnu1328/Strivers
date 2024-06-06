# Longest Increasing Subsequence

[Problem Link](https://www.geeksforgeeks.org/problems/longest-increasing-subsequence-1587115620/1)

## Approach - 
1. We solved this same problem, previously, but there we need to solve this problem in ```O(N log N)```.
2. How do solve this problem with that complexity, with the help of binary Search
3. As we observe, in LIS the array is sorted, with this we can use binary search.
4. Find the index of element that is part of LIS, and try to find the maximum lastIndex.
5. finally return lastIndex + 1

```Java


class Solution
{
    public:
    
    int binarySearch(vector<int> &dp, int low, int high, int value) {
        
        if(value > dp[high]) return high + 1;
        
        while(low < high) {
            int mid = (low + high)/2;
            
            if(dp[mid] == value) return mid;
            
            else if(dp[mid] > value) high = mid;
            
            else low = mid + 1;
        }
        
        return high;
    }
    
    //Function to find length of longest increasing subsequence.
    int longestSubsequence(int n, int a[])
    {
       vector<int> dp(n);
       dp[0] = a[0];
       
       int lastIndex = 0;
       
       for(int i=1; i<n; i++) {
           //get the far possible index for a[i]
           
           int index = binarySearch(dp, 0, lastIndex, a[i]);
           
           dp[index] = a[i];
           
           lastIndex = max(lastIndex, index);
       }
       
       return lastIndex+1;
    }
};


```

## Complexity Analysis

### Time complexity: O(N*log(N))

### Space Compleixty: O(N) 