# Largest subarray with 0 sum

[Problem Link](https://www.geeksforgeeks.org/problems/largest-subarray-with-0-sum/1)

## Approach - 1

1. Find sum for all sub-arrays, and check if sum is equal to zero, then maximize the answer(length)

## Complexity Analysis:

### Time Complexity: O(N^2)

### Space Complexity: O(1)

## Approach - 2

1. Use hashmap and prefix Sum concepts
2. Find prefix sum for the given array, and check if the prefixSum is exit in the map
3. If exit, then find the length of it
4. else put the element with its index in map

```Java

class GfG
{
    int maxLen(int arr[], int n)
    {
        // Your code here
        Map<Integer, Integer> prefixSum = new HashMap<>();

        int sum = 0;
        int ans = 0;

        for(int i=0; i<n; i++) {
            sum += arr[i];

            if(sum == 0) {
                ans = Math.max(ans, i + 1);
            }

            if(!prefixSum.containsKey(sum)) {
                prefixSum.put(sum, i);
            } else {
                ans = Math.max(ans, i - prefixSum.get(sum));
            }
        }

        return ans;
    }
}

```

## Complexity Analysis:

### Time Complexity: O(N)

### Space Complexity: O(N)
