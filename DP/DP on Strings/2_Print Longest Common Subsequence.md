# Print Longest Common Subsequence

[Problem Link](https://www.codingninjas.com/studio/problems/print-longest-common-subsequence_8416383?utm_source=striver&utm_medium=website&utm_campaign=a_zcoursetuf&leftPanelTabValue=PROBLEM)

## Recurssion

1. This problem is same as Longest Common subsequence problem
2. But, here we need to return Lognest common subsequence string

```Java

public class Solution {

    static String solve(int i, int j, String s1, String s2, String dp[][]) {
        if(i < 0 || j < 0) return "";


        if(s1.charAt(i) == s2.charAt(j)) {
            String curr = "";
            curr = curr + s1.charAt(i) + solve(i-1, j-1, s1, s);
            return curr;
        }

        else {
            String curr = solve(i-1, j, s1, s2);
            String curr1 = solve(i, j-1, s1, s2);

            if(curr.length() > curr1.length()) {
                return curr;
            }

            return curr1;
        }
    }

    public static String findLCS(int n, int m, String s1, String s2){


        return solve(n-1, m-1, s1, s2);
    }
}

```

## Complexity Analysis:

### Time Complexity: O(2^N)

### Space Complexity: O(N) (Stack Space)

## Memoization

```Java

public class Solution {

    static String solve(int i, int j, String s1, String s2, String dp[][]) {
        if(i < 0 || j < 0) return "";

        if(dp[i][j] != "") return dp[i][j];

        if(s1.charAt(i) == s2.charAt(j)) {
            String curr = "";
            curr = curr + s1.charAt(i) + solve(i-1, j-1, s1, s2,dp);
            return dp[i][j] = curr;
        }

        else {
            String curr = solve(i-1, j, s1, s2, dp);
            String curr1 = solve(i, j-1, s1, s2, dp);

            if(curr.length() > curr1.length()) {
                return dp[i][j] = curr;
            }

            return dp[i][j] = curr1;
        }
    }

    public static String findLCS(int n, int m, String s1, String s2){

        String dp[][] = new String[n][m];

        for(int i=0; i<n; i++) {
            for(int j=0; j<m; j++) {
                dp[i][j] = "";
            }
        }

        return solve(n-1, m-1, s1, s2, dp);
    }
}

```

## Complexity Analysis:

### Time Complexity: O(N\*M)

### Space Complexity: O(N\*M) + O(N) (Stack Space)

## Tabulation

```Java

public class Solution {

    public static String findLCS(int n, int m, String s1, String s2){

        String dp[][] = new String[n+1][m+1];

        for(int i=0; i<=n; i++) {
            for(int j=0; j<=n; j++) {
                if(i == 0 || j==0) {
                    dp[i][j] = "";
                    continue;
                }

                if(s1.charAt(i) == s2.charAt(j)) {
                    dp[i][j] = s1.charAt(i) + dp[i-1][j-1];
                } else {
                    String curr = dp[i-1][j];
                    String curr1 = dp[i][j-1];

                    if(curr.length() > curr1.length()) {
                        dp[i][j] = curr;
                    } else {
                        dp[i][j] = curr1;
                    }
                }
            }
        }

        return dp[n][m];
    }
}

```

## Complexity Analysis:

### Time Complexity: O(N\*M)

### Space Complexity: O(N\*M)

## Space Optimization

```Java

public class Solution {


    public static String findLCS(int n, int m, String s1, String s2){

        String prev[] = new String[n+1];
        String cur[] = new String[m+1];

        for(int i=0; i<=n; i++) {
            prev[i] = "";
        }

        for(int i=1; i<=n; i++) {
            for(int j=1; j<=m; j++) {

                if(s1.charAt(i-1) == s2.charAt(j-1)) {
                    cur[j] = s1.charAt(i-1) + prev[j-1];
                } else {
                    String curr = prev[j];
                    String curr1 = cur[j-1];

                    if(curr.length() > curr1.length()) {
                        cur[j] = curr;
                    } else {
                        cur[j] = curr1;
                    }
                }
            }

            for(int j=1; j<=m; j++) {
                prev[j] = cur[j];
            }
        }

        return prev[m];
    }
}

```

## Complexity Analysis:

### Time Complexity: O(N\*M)

### Space Complexity: O(M)
