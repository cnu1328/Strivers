# Number of Coins

[Problem Link](https://www.geeksforgeeks.org/problems/number-of-coins1824/1)

## Approach - 1

1. sort the given coins array
2. Then Traverse it, if a coin value is less the given amount
3. Try try to get as possible amount and reduce this amount from given amount
4. Do for all coins

```c++

class Solution{

	public:
	int minCoins(vector<int> &coins, int n, int amount)
	{
	    sort(coins.begin(), coins.end(), greater<int>());

	    int ans = 0;

	    for(int i=0; i<n; i++) {
	        if(coins[i] <= amount) {
	            int count = amount / coins[i];
	            ans += count;
	            amount = amount - (count * coins[i]);
	        }
	    }

	    if(amount != 0) return -1;

	    return ans;

	}

};

```

## Complexity Analysis:

### Time Complexity: O(Log N + N)

### Space Complexity: (1)
