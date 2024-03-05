# Coin Change II

[Problem Link]()

## Recurssion

```Java

class Solution {
public:

    int solve(int n, int amount, vector<int>& coins) {
        if(amount == 0) return 1;
        if(n < 0) return 0;

        int notTake = solve(n-1, amount, coins);
        int take = 0;
        if(coins[n] <= amount) {
            take = solve(n, amount - coins[n], coins);
        }

        return (take + notTake);
    }

    int change(int amount, vector<int>& coins) {
        int n = coins.size();

        return solve(n-1, amount, coins);
    }
};

```

## Complexity Analysis:

### Time Complexity: O(2^N)

### Space Complexity: O(N)

## Memoization

```Java

class Solution {
public:

    int solve(int n, int amount, vector<int>& coins, vector<vector<int>>& dp) {
        if(amount == 0) return 1;
        if(n < 0) return 0;

        if(dp[n][amount] != -1) return dp[n][amount];

        int notTake = solve(n-1, amount, coins, dp);
        int take = 0;
        if(coins[n] <= amount) {
            take = solve(n, amount - coins[n], coins, dp);
        }

        return dp[n][amount] = (take + notTake);
    }

    int change(int amount, vector<int>& coins) {
        int n = coins.size();
        vector<vector<int>> dp(n, vector<int> (amount + 1, -1));
        return solve(n-1, amount, coins, dp);
    }
};

```

## Complexity Analysis:

### Time Complexity: O(N\*Amount)

### Space Complexity: O(N\*Amount) + O(N)

## Tabulation

```C++

class Solution {
public:

    int change(int amount, vector<int>& coins) {
        int n = coins.size();
        vector<vector<int>> dp(n, vector<int> (amount + 1, 0));

        for(int i=0; i<n; i++) {
            dp[i][0] = 1;
        }

        for(int i=0; i<=amount; i++) {
            if(i%coins[0] == 0)
                dp[0][i] = 1;
        }


        for(int i=1; i<n; i++) {
            for(int j = 1; j<=amount; j++) {
                int notTake = dp[i-1][j];
                int take = 0;

                if(coins[i] <= j) {
                    take = dp[i][j-coins[i]];
                }

                dp[i][j] = (take + notTake);
            }
        }

        return dp[n-1][amount];

    }
};

```

## Complexity Analysis:

### Time Complexity: O(N\*Amount)

### Space Complexity: O(N\*Amount)

## Space Optimization

```C++

class Solution {
public:


    int change(int amount, vector<int>& coins) {
        int n = coins.size();
        vector<int> prev(amount + 1, 0);
        vector<int> curr(amount + 1, 0);

        prev[0] = 1;
        curr[0] = 1;

        for(int i=0; i<=amount; i++) {
            if(i%coins[0] == 0)
                prev[i] = 1;
        }


        for(int i=1; i<n; i++) {
            for(int j = 1; j<=amount; j++) {
                int notTake = prev[j];
                int take = 0;

                if(coins[i] <= j) {
                    take = curr[j-coins[i]];
                }

                curr[j] = (take + notTake);
            }

            prev = curr;
        }

        return prev[amount];

    }
};

```

## Complexity Analysis:

### Time Complexity: O(N\*Amount)

### Space Complexity: O(Amount)
