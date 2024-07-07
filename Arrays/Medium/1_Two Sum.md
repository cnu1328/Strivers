# 1. Two Sum

[Problem Link](https://leetcode.com/problems/two-sum/)

## Approach - 1

1. Check for every number, if you add other number that equals to target, then return its indices

```Java

for(int i=0; i<n; i++) {
    for(int j=i+1; j<n; j++) {
        if(arr[i] + arr[j] == target) return {i, j};
    }
}

```

## Complexity Analysis:

### Time Complexity: O(N^2)

### Space Complexity: O(1)

## Approach - 2

1. Use Hash Map
2. For every number, check in the map, `target-nums[i]` present or not, if present then `i and index in the map`
3. If not found, then insert the nums[i] to the map with its index i

```Java

class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {

        map<int, int> mp;

        vector<int> v;

        for(int i = 0; i < nums.size(); i++) {

            int a = nums[i];
            int remain = target - a;

            if(mp.find(remain)!=mp.end()) {
                v.push_back(mp[remain]);
                v.push_back(i);
                break;
            }

            mp[a] = i;

        }

        return v;
    }
};

```

## Complexity Analysis:

### Time Complexity: O(N \* log N)

### Space Complexity: O(N)

## Approach - 3 - sort and find

1. First sort the array
2. Declare variables as left = 0 and right = n-1
3. If `nums[left] + nums[right]` > target then perform `right--`
4. else `left++`
5. If you find two sum equal to target return the indices

```Java

public static String twoSum(int n, int []arr, int target) {
    Arrays.sort(arr);
    int left = 0, right = n - 1;
    while (left < right) {
        int sum = arr[left] + arr[right];
        if (sum == target) {
            return "YES";
        } else if (sum < target) left++;
        else right--;
    }
    return "NO";
}

```

## Complexity Analysis:

### Time Complexity: O(N \* log N)

### Space Complexity: O(1)
