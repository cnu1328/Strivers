# Longest Common Substring

[Problem Link](https://www.codingninjas.com/studio/problems/longest-common-substring_1235207?utm_source=striver&utm_medium=website&utm_campaign=a_zcoursetuf&leftPanelTabValue=PROBLEM)

## Tabulation

1. As we are aware about the Longest Common Subsequence, it is very similar to that, but here we will find the Longest Common Substring.
2. As substring is Continuous in nature, we need to find LCS
3. The the characters matches then decrement i-1 and j-1
4. otherwise put i-1 and j-1 zero value

<img width="738" alt="image" src="https://github.com/user-attachments/assets/63730c32-c8da-41ac-939d-ec58d9510231">


```Java

public class Solution {
    public static int lcs(String str1, String str2){
        // Write your code here.

        int n = str1.length();
        int m = str2.length();

        int dp[][] = new int[n+1][m+1];

        int ans = 0;

        for(int i=1; i<=n; i++) {
            for(int j=1; j<=m; j++) {
                if(str1.charAt(i-1) == str2.charAt(j-1)) {
                    dp[i][j] = 1 + dp[i-1][j-1];
                    ans = Math.max(dp[i][j], ans);
                } else {
                    dp[i][j] = 0;
                }
            }
        }

        return ans;
    }
}


```

## Complexity Analysis:

### Time Complexity: O(N\*M)

### Space Complexity: O(N\*M)


## Space Optimization

```Java

public class Solution {
    public static int lcs(String str1, String str2){
        // Write your code here.

        int n = str1.length();
        int m = str2.length();

        int prev[] = new int[m+1];
        int curr[] = new int[m+1];
        

        int ans = 0;

        for(int i=1; i<=n; i++) {
            for(int j=1; j<=m; j++) {
                if(str1.charAt(i-1) == str2.charAt(j-1)) {
                    curr[j] = 1 + prev[j-1];
                    ans = Math.max(curr[j], ans);
                } else {
                    curr[j] = 0;
                }
            }

            for(int j=0; j<=m; j++) {
                prev[j] = curr[j];
            }
        }

        return ans;
    }
}

```

## Complexity Analysis:

### Time Complexity: O(N\*M)

### Space Complexity: O(M)
