# Print Longest Increasing Subsequence

[Problem Link](https://www.geeksforgeeks.org/problems/printing-longest-increasing-subsequence/1)

## Approach - Use Tabulation
1. use Tabulation approach to find the longest LIS
2. Then, take a new hash, which points the LIS lastIndex, which form a chain like => suppose lastIndex is 3, then at index 3 we have other number like 2 and then at index 2 we have other index that is 0

Finally => 3 -> 2 -> 0

3. Chack the condition like arr[prev] < arr[ind] (to check ```ind``` is part of LIS) and Maximum length LIS, If satisfies go and modify the dp[ind] and hash[ind]

4. if you get any maximum length, the try to hold the index in lastIndex variable
5. After all, traverse from last index and store all in a vector, reverse the vector and return that vector.


```Java


class Solution {
  public:
    vector<int> longestIncreasingSubsequence(int n, vector<int>& arr) {
        vector<int> dp(n, 1), hash(n);
        int lastInd = 0;
        int maxi = 1;
        
        
        for(int ind = 0; ind < n; ind++) {
            
            hash[ind] = ind;
            
            for(int prev=0; prev < ind; prev++) {
                
                if(arr[prev] < arr[ind] && (1 + dp[prev]) > dp[ind]) {
                    dp[ind] =  1 + dp[prev];
                    hash[ind] = prev;
                }
            }
            
            if(dp[ind] > maxi) {
                maxi = dp[ind];
                lastInd = ind;
            }
        }
        
        
        vector<int> ans;
        
        ans.push_back(arr[lastInd]);
        
        while(hash[lastInd] != lastInd) {
            lastInd = hash[lastInd];
            ans.push_back(arr[lastInd]);
        }
        
        reverse(ans.begin(), ans.end());
        
        return ans;
        
        
    }
};

```

## Complexity Analysis

### Time complexity: O(N*N)

### Space Compleixty: O(N) 