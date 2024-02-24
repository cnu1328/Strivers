# Array partition with minimum difference

[Problem Link](https://www.codingninjas.com/studio/problems/partition-a-set-into-two-subsets-such-that-the-difference-of-subset-sums-is-minimum._842494?utm_source=striver&utm_medium=website&utm_campaign=a_zcoursetuf&leftPanelTabValue=PROBLEM)

## Intuition

1. This problem is completely depends upon the idea of `sum of subset is equal to target `.
2. We find the tabulation for sum of subset equal to target problem.
3. The last row in the dp specifies that the subset sum is possible or not possible.
4. If one subset sum is found with the help of dp last row, then we can easily find other subset sum, example `subset2 sum = Total array sum - subset 1 sum`.
5. Finally, we can calculate the minimum absolute value

## Code

```Java

public class Solution {
    public static int minSubsetSumDifference(int []nums, int n) {
        int sum = 0;

        for(int i=0; i<n; i++) {
            sum += nums[i];
        }

        boolean dp[][] = new boolean[n][sum + 1];

        for(int i=0; i<n; i++) {
            for(int j = 0; j<=sum; j++) {
                dp[i][j] = false;
            }
        }

        for(int i=0; i<n; i++) {
            dp[i][0] = true;
        }

        if(sum > 0 && nums[0] <= sum) dp[0][nums[0]] = true;

        for(int i=1; i<n; i++) {
            for(int target = 1; target <= sum; target++){
                boolean notTake = dp[i-1][target];

                boolean Take  = false;

                if(nums[i] <= target) Take = dp[i-1][target - nums[i]];

                dp[i][target] = (notTake | Take);
            }
        }

        int ans = 1000000000;

        for(int i=0; i<=sum; i++) {

            if(dp[n-1][i]) {
                int sum1 = i;
                int sum2 = sum - i;

                ans = Math.min(ans, Math.abs(sum1 - sum2));
            }
        }

        return ans;
    }
}

```

## Complexity Anaysis:

### Time Coplexity: O(N\*sum)

### Space Complexity: O(N\*sum) + O(sum)

## Space Optimization

```Java

public class Solution {
    public static int minSubsetSumDifference(int []nums, int n) {
        int sum = 0;

        for(int i=0; i<n; i++) {
            sum += nums[i];
        }

        boolean dp[][] = new boolean[n][sum/2 + 1];

        for(int i=0; i<n; i++) {
            for(int j = 0; j<=sum/2; j++) {
                dp[i][j] = false;
            }
        }

        for(int i=0; i<n; i++) {
            dp[i][0] = true;
        }

        if(nums[0] <= sum/2) dp[0][nums[0]] = true;

        for(int i=1; i<n; i++) {
            for(int target = 1; target <= sum/2; target++){
                boolean notTake = dp[i-1][target];

                boolean Take  = false;

                if(nums[i] <= target) Take = dp[i-1][target - nums[i]];

                dp[i][target] = (notTake | Take);
            }
        }

        int ans = 1000000000;

        for(int i=0; i<=sum/2; i++) {

            if(dp[n-1][i]) {
                int sum1 = i;
                int sum2 = sum - i;

                ans = Math.min(ans, Math.abs(sum1 - sum2));
            }
        }

        return ans;
    }
}

```

## Complexity Anaysis:

### Time Coplexity: O(N\*(sum/2))

### Space Complexity: O(N\*(sum/2)) + O(sum/2)