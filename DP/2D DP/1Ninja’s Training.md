# Ninja’s Training

[Problem Link](https://www.codingninjas.com/studio/problems/ninja%E2%80%99s-training_3621003?utm_source=striver&utm_medium=website&utm_campaign=a_zcoursetuf)

## Approach(Recurssion)

1. Choose the index as dates, and think of which one variable is required to make sure that consecutive work can't be done. That is last variable

2. Now, think of base case that is, if day is equal to zero it reached at end, we return maximum value from other activities other than last index activity

3. else, we check the same for other days.

4. return maximum of profit value

## Code

```Java

public class Solution {

    static int maxMerit(int day, int last, int points[][]) {

        if(day == 0) {
            int maxi = 0;

            for(int i=0; i<=2; i++) {
                if(i != last) {
                    maxi = Math.max(maxi, points[0][i]);
                }
            }

            return maxi;
        }

        int maxi = 0;

        for(int i=0; i<=2; i++) {
            if(i != last) {
                int profit = points[day][i] + maxMerit(day-1, i, points);

                maxi = Math.max(maxi, profit);
            }
        }

        return maxi;
    }

    public static int ninjaTraining(int n, int points[][]) {

        return maxMerit(n-1, 3, points);
    }

}

```

## Complexity Analysis

### Time Complexity: O(exponential)

### Space Complexity: O(N)

## Memoization

```Java

public class Solution {

    static int maxMerit(int day, int last, int points[][], int dp[][]) {

        if(day == 0) {
            int maxi = 0;

            for(int i=0; i<=2; i++) {
                if(i != last) {
                    maxi = Math.max(maxi, points[0][i]);
                }
            }

            return maxi;
        }

        if(dp[day][last] != -1) return dp[day][last];

        int maxi = 0;

        for(int i=0; i<=2; i++) {
            if(i != last) {
                int profit = points[day][i] + maxMerit(day-1, i, points, dp);

                maxi = Math.max(maxi, profit);
            }
        }

        return dp[day][last] = maxi;
    }

    public static int ninjaTraining(int n, int points[][]) {
        int dp[][] = new int[n][4];

        for(int i=0; i<n; i++) {
            for(int j=0; j<4; j++) {
                dp[i][j] = -1;
            }
        }
        return maxMerit(n-1, 3, points, dp);
    }

}

```

## Complexity Analysis

### Time Complexity: O(N*4*3) 4 for dp array and 3 for looping 0..2 in every recurssion call

### Space Complexity: O(N) + O(N\*4)

- **Now We develop Tabulation to reduce stack space complexity**

## Tabulation

```Java

public class Solution {
   public static int ninjaTraining(int n, int points[][]) {

       int dp[][] = new int[n][4];

       dp[0][0] = Math.max(points[0][1], points[0][2]);
       dp[0][1] = Math.max(points[0][0], points[0][2]);
       dp[0][2] = Math.max(points[0][0], points[0][1]);
       dp[0][3] = Math.max(points[0][0], Math.max(points[0][1], points[0][2]));

       for(int day = 1; day<n; day++) {
           for(int last = 0; last<4; last++) {

               dp[day][last] = 0;

               for(int task = 0; task < 3; task++) {

                   if(task != last) {
                       int profit = points[day][task] + dp[day-1][task];

                       dp[day][last] = Math.max(dp[day][last], profit);
                   }

               }

           }
       }

       return dp[n-1][3];
   }

}
```

## Complexity Analysis

### Time Complexity: O(N*4*3) 4 for dp array and 3 for looping 0..2 in every recurssion call

### Space Complexity: O(N\*4)

## Space Optimization

```Java

public class Solution {
    public static int ninjaTraining(int n, int points[][]) {

        int dp[] = new int[4];

        dp[0] = Math.max(points[0][1], points[0][2]);
        dp[1] = Math.max(points[0][0], points[0][2]);
        dp[2] = Math.max(points[0][0], points[0][1]);
        dp[3] = Math.max(points[0][0], Math.max(points[0][1], points[0][2]));

        for(int day = 1; day<n; day++) {

            int curr[] = new int[4];

            for(int last = 0; last<4; last++) {

                curr[last] = 0;

                for(int task = 0; task < 3; task++) {

                    if(task != last) {
                        int profit = points[day][task] + dp[task];

                        curr[last]= Math.max(curr[last], profit);
                    }

                }

            }

            for(int i=0; i<4; i++) {
                dp[i] = curr[i];
            }
        }

        return dp[3];
    }

}

```
