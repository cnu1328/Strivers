# Fruit Into Baskets

[Problem LInk](https://www.geeksforgeeks.org/problems/fruit-into-baskets-1663137462/1)

## Approach - 1

1. Use map, if map size is greater than the two baskets, then try to trim the window from left
2. return the max length

```Java

class Solution {
  public:
    int totalFruits(vector<int> &arr) {

        map<int, int> mp;

        int left = 0, right = 0, ans = 0;
        int basket = 2;

        while(right < arr.size()) {
            mp[arr[right]]++;

            while(mp.size() > basket) {

                mp[arr[left]]--;

                if(mp[arr[left]] == 0) {
                    mp.erase(arr[left]);
                }

                left++;

            }

            ans = max(ans, right - left + 1);
            right++;
        }

        return ans;
    }
};

```

## Complexity Analysis

### Time Complexity: O(N)

### Space Complexity: O(1)
