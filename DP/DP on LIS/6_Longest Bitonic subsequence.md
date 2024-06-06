# Longest Bitonic subsequence

[Problem Link](https://www.geeksforgeeks.org/problems/longest-bitonic-subsequence0824/1)


## Approach

1. The Longest Bitonic Subsequence is nothing but, numbers strictly increases to certain index and then decreases.
2. And also, only increases and decreases
3. Here, In this question mentioned only 1st point.
4. To solve this, first find the Longest Increasing Subsequence from index 0 to n-1
5. And, find the Longest Increasing Subsequence from n-1 to 0
6. After that, if dp1[i] > 1 and dp2[i] > 1, then taken the dp values into consideration into answer, with max dp value
7. finally return Longest Bitonic Subsequence


```Java

class Solution {
  public:
    int LongestBitonicSequence(int n, vector<int> &arr) {
        // code here
        
        int ans = 0;
        
        vector<int> dp1(n, 1), dp2(n, 1);
        
        
        for(int i=0; i<n; i++) {
            
            
            for(int prev = 0; prev < i; prev++) {
                
                if(arr[i] > arr[prev] && (dp1[prev] + 1) > dp1[i]) {
                    dp1[i] = dp1[prev] + 1;
                }
            }
        }
        
        for(int ind = n-1; ind >= 0; ind--) {
            for(int prev = n-1; prev > ind; prev--) {
                
                if(arr[ind] > arr[prev] && (dp2[prev] + 1) > dp2[ind]) {
                    dp2[ind] = dp2[prev] + 1;
                }
            }
        }
        
        for(int i=0; i<n-1; i++) {
            
            if(dp1[i] > 1 && dp2[i] > 1)
                ans = max(ans, dp1[i] + dp2[i] - 1);
        }
        
        
        return ans;
        
        
        
    }
};

```



## Complexity Analysis:

### Time Complexity : O(N*N)
### Space Complexity: O(N)