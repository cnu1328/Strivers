# Boolean Evaluation

[Problem Link](https://www.naukri.com/code360/problems/problem-name-boolean-evaluation_1214650?leftPanelTabValue=SUBMISSION)


## Approach - Reucurssion (Top Down Approach)

1. Here, we need to the find the number of boolean evaluation that results to true
2. In the expression, we have three operands, or, and and xor.
3. lets take ```and```, here to get number of true results get by total number of trues on left side multiplied by total number of true's on right side.
    - For true's => ```left & rigth```
        - total = ```LT * RT```
    - For False => ```(LT * RF) + (RT * LF) + (RF *TF)```
4. For ```or``` operator, 
    - For true's => ```(LT*RF) + (LT*RT) + (RT*LF)```
    - For false => ```(LT*RF)```
5. For ```xor```
    - For true's => ```(LT*RF) + (LF*RT)```
    - For false => ```(RT*LT) + (RF*LF)```

6. sum of all the ways, and return the answer

```Java

#define ll long long int

int mod = 1e9 + 7;

ll findWays(int i, int j, bool isTrue, string &exp) {

    if(i > j) return 0;


    if(i == j) {
        if(isTrue) return exp[i] == 'T';
        return exp[i] == 'F';
    }

    ll ways = 0;

    for(int ind = i+1; ind <= j-1; ind = ind+2) {
        ll lt = findWays(i, ind -1, 1, exp);
        ll lf = findWays(i, ind-1, 0, exp);
        ll rt = findWays(ind+1, j, 1, exp);
        ll rf = findWays(ind+1, j, 0, exp);

        if(exp[ind] == '&') {
            if(isTrue) ways = (ways +  (lt * rt)%mod)%mod;

            else ways = (ways + (lt * rf)%mod + (lf * rt)%mod + (lf * rf)%mod)%mod;
        }

        else if(exp[ind] == '|') {
            if(isTrue) ways = (ways + (lt*rt)%mod + (lf * rt)%mod + (rf * lt)%mod)%mod;
            else ways = (ways + (lf * rf)%mod)%mod;
        }

        else {
            if(isTrue) ways = (ways + (rt*lf)%mod + (rf*lt)%mod)%mod;

            else ways = (ways + (rt*lt)%mod + (rf*lf)%mod)%mod;
        }
    }

    return ways;

}

int evaluateExp(string & exp) {
    // Write your code here.
    int n = exp.length();
    return findWays(0, n-1, 1, exp);

}

```

## Complexity Analysis:

### Time Complexity : O(exponential)
### Space Complexity: O(N)


## Memoization(Top Down Approach)

1. Use 3D Dp array

```Java

#define ll long long 

int mod = 1e9 + 7;

ll findWays(int i, int j, bool isTrue, string &exp, vector<vector<vector<ll>>> &dp) {

    if(i > j) return 0;


    if(i == j) {
        if(isTrue) return exp[i] == 'T';
        return exp[i] == 'F';
    }

    if(dp[i][j][isTrue] != -1) return dp[i][j][isTrue];

    ll ways = 0;

    for(int ind = i+1; ind <= j-1; ind = ind+2) {
        ll lt = findWays(i, ind -1, 1, exp, dp);
        ll lf = findWays(i, ind-1, 0, exp, dp);
        ll rt = findWays(ind+1, j, 1, exp, dp);
        ll rf = findWays(ind+1, j, 0, exp, dp);

        if(exp[ind] == '&') {
            if(isTrue) ways = (ways +  (lt * rt)%mod)%mod;

            else ways = (ways + (lt * rf)%mod + (lf * rt)%mod + (lf * rf)%mod)%mod;
        }

        else if(exp[ind] == '|') {
            if(isTrue) ways = (ways + (lt*rt)%mod + (lf * rt)%mod + (rf * lt)%mod)%mod;
            else ways = (ways + (lf * rf)%mod)%mod;
        }

        else {
            if(isTrue) ways = (ways + (rt*lf)%mod + (rf*lt)%mod)%mod;

            else ways = (ways + (rt*lt)%mod + (rf*lf)%mod)%mod;
        }
    }

    return dp[i][j][isTrue] = ways;

}

int evaluateExp(string & exp) {
    // Write your code here.
    int n = exp.length();

    vector<vector<vector<ll>>> dp(n, vector<vector<ll>>(n, vector<ll> (2, -1)));

    return findWays(0, n-1, 1, exp, dp);

}

```


## Complexity Analysis:

### Time Complexity : O(N*N*2)*N => (N^3)
### Space Complexity: O(N*N*2) + O(N)


## Tabulation ( Bottom Up Approach)


```Java


#define ll long long 

int mod = 1e9 + 7;

int evaluateExp(string & exp) {
    // Write your code here.
    int n = exp.length();

    vector<vector<vector<ll>>> dp(n, vector<vector<ll>>(n, vector<ll> (2, 0)));

    for(int i = n-1; i>=0; i--) {
        for(int j=0; j<=n-1; j++) {
            for(int isTrue = 0; isTrue < 2; isTrue++) {

                if(i == j) {
                    if(isTrue) dp[i][j][isTrue] = exp[i] == 'T';

                    else dp[i][j][isTrue] = exp[i] == 'F';

                    continue;
                }


                ll ways = 0;

                for(int ind = i+1; ind <= j-1; ind = ind+2) {
                    ll lt = dp[i][ind -1][1];
                    ll lf =dp[i][ind-1][0];
                    ll rt = dp[ind+1][j][1];
                    ll rf = dp[ind+1][j][0];

                    if(exp[ind] == '&') {
                        if(isTrue) ways = (ways +  (lt * rt)%mod)%mod;

                        else ways = (ways + (lt * rf)%mod + (lf * rt)%mod + (lf * rf)%mod)%mod;
                    }

                    else if(exp[ind] == '|') {
                        if(isTrue) ways = (ways + (lt*rt)%mod + (lf * rt)%mod + (rf * lt)%mod)%mod;
                        else ways = (ways + (lf * rf)%mod)%mod;
                    }

                    else {
                        if(isTrue) ways = (ways + (rt*lf)%mod + (rf*lt)%mod)%mod;

                        else ways = (ways + (rt*lt)%mod + (rf*lf)%mod)%mod;
                    }
                }

               dp[i][j][isTrue] = ways;
            }
        }
    }

    return dp[0][n-1][1];

}

```


## Complexity Analysis:

### Time Complexity : O(N*N*2)*N => (N^3)
### Space Complexity: O(N*N*2)





