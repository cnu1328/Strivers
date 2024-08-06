# 42. Trapping Rain Water

[Problem Link](https://leetcode.com/problems/trapping-rain-water/)

## Approach - 1

1. First take two arrays, left and right
2. Then Find the maximum till index i from 0 to n-1 and store them in left array
3. Find the maximum height till index i from n-1 to 0 and store them in right array
4. Traverse the array again and find minimum from both left and right array at particular index i
5. answer += min(left[i], right[i]) - height[i]
6. return the answer

```c++

class Solution {
    public int trap(int[] height) {
        int n = height.length;

        int left[] = new int[n], right[] = new int[n];

        left[0] = height[0];
        right[n-1] = height[n-1];

        for(int i=1; i<n; i++) {
            left[i] = Math.max(left[i-1], height[i]);
        }

        for(int i=n-2; i>=0; i--) {
            right[i] = Math.max(right[i+1], height[i]);
        }

        int ans = 0;

        for(int i=0; i<n; i++) {
            ans += Math.min(left[i], right[i]) - height[i];
        }

        return ans;
    }
}

```

## Complexity Analysis:

### Time Complexity: O(N)

### Space Complexity: (1)

## Approach - 2

1. Use two pointers, one is left and other one is right
2. check if the height[left] <= hegiht[right]
   - check if the height[left] >= leftMax
     - leftMax = height[left]
   - else ans += leftMax - height[left];
3. else
   - check if the height[right] >= rightMax
     - rightMax = height[right]
   - else ans += rightMax - height[right];
4. return the answer

```c++

class Solution {
    public int trap(int[] height) {
        int n = height.length;

        int left =0, right = n-1;
        int ans = 0, leftMax = 0, rightMax = 0;

        while(left <= right) {

            if(height[left] <= height[right]) {
                if(height[left] >= leftMax) {
                    leftMax = height[left];
                } else {
                    ans += (leftMax - height[left]);
                }

                left++;
            }

            else {
                if(height[right] >= rightMax) {
                    rightMax = height[right];
                }

                else {
                    ans += (rightMax - height[right]);
                }

                right--;
            }
        }

        return ans;
    }
}

```

## Complexity Analysis:

### Time Complexity: O(N)

### Space Complexity: (1)
