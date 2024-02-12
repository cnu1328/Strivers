# House Robber II

[Problem Link](https://leetcode.com/problems/house-robber-ii/description/)

[Problem Link](https://www.codingninjas.com/studio/problems/house-robber-ii_839733?utm_source=striver&utm_medium=website&utm_campaign=a_zcoursetuf)


```Java

class Solution {

    int maximum(ArrayList<Integer> nums) {
        int prev = 0, prev2 = 0;
        int n = nums.size();;

        int dp[] = new int[n];
        dp[0] = nums.get(0);

        for(int i=1; i<n; i++) {
            int pick = nums.get(i);

            if(i > 1) pick += dp[i-2];

            int notpick = dp[i-1];

            dp[i] = Math.max(pick, notpick);
        }

        return dp[n-1];
    }

    public int rob(int[] nums) {
        int n = nums.length;

        if(n == 1) return nums[0];

        ArrayList<Integer> temp1 = new ArrayList<>();
        ArrayList<Integer> temp2 = new ArrayList<>();

        for(int i=0; i<n; i++) {
            if(i != 0) temp1.add(nums[i]);
            if(i != n-1) temp2.add(nums[i]);
        }
        int ans1 = maximum(temp1);
        int ans2 = maximum(temp2);

        return Math.max(ans1, ans2);
    }
}

```


