# 132. Palindrome Partitioning II

[Problem Link](https://leetcode.com/problems/palindrome-partitioning-ii/)

## Approach - Recurssive ( Top Down Approach)

1. To solve this problem, use ```Front Partition```, it specifies that, start from index 0, partition for every further indices if at particular index satisfies the condition.
2. Find the minimum among all the possiblilies
3. return the answer by removing one from answer, because, for every index, it is partitioning, so answer will be one more than real answer.

```C++

class Solution {
public:
    
    
    bool isPalin(int left, int right, string temp) {
        
        while(left <= right) {
            if(temp[left++] != temp[right--]) return false;
        }
        
        return true;
    }
    
    int solve(int ind, string s) {
        
        if(ind == s.length()) return 0;
        
        int mini = INT_MAX;
        
        
        
        for(int j = ind; j < s.length(); j++) {
            
            
            if(isPalin(ind, j, s)) {
                int cost = 1 + solve(j+1, s);
                
                mini = min(mini, cost);
            }
            
        }
        
        return mini;
    }
    
    int minCut(string s) {
        
        return solve(0, s) - 1;
    }
};

```

## Complexity Analysis:

### Time Complexity : O(expoential) but TLE
### Space Complexity: O(N)


## Memoization - (Top Down Approach)

```C++

class Solution {
public:
    
    
    bool isPalin(int left, int right, string &temp) {
        
        while(left <= right) {
            if(temp[left++] != temp[right--]) return false;
        }
        
        return true;
    }
    
    int solve(int ind, string s, vector<int> &dp) {
        
        if(ind == s.length()) return 0;
        
        if(dp[ind] != -1) return dp[ind];
        
        int mini = INT_MAX;
        
        
        
        for(int j = ind; j < s.length(); j++) {
            
            
            if(isPalin(ind, j, s)) {
                int cost = 1 + solve(j+1, s, dp);
                
                mini = min(mini, cost);
            }
            
        }
        
        return dp[ind] = mini;
    }
    
    int minCut(string s) {
        
        vector<int> dp(s.length(), -1);
        
        return solve(0, s, dp) - 1;
    }
};

```

## Complexity Analysis:

### Time Complexity : O(N*N)
### Space Complexity: O(N) + (N) 


## Tabulation (Bottom - UP Appraoch)

```C++

class Solution {
public:
    
    
    bool isPalin(int left, int right, string &temp) {
        
        while(left <= right) {
            if(temp[left++] != temp[right--]) return false;
        }
        
        return true;
    }
    
    
    
    int minCut(string s) {
        
        int n = s.length();
        vector<int> dp(n+1, 0);
        
        for(int ind = n-1; ind >= 0; ind--) {
            int mini = INT_MAX;
        
            for(int j = ind; j < s.length(); j++) {


                if(isPalin(ind, j, s)) {
                    int cost = 1 + dp[j+1];

                    mini = min(mini, cost);
                }

            }

            dp[ind] = mini;
        }
        
        
        
        return dp[0] - 1;
    }
};

```


## Complexity Analysis:

### Time Complexity : O(N*N)
### Space Complexity: O(N)



