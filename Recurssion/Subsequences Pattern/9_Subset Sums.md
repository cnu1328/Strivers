# Subset Sums


[Problem Link](https://www.geeksforgeeks.org/problems/subset-sums2234/1)

## Approach - Pick and Not pick element

1. Implement the pick and not pick approach
2. While picking the element, increment the sum by element
3. return the answer

```Java

class Solution {
    
    void subsum(int index, int sum, int n, ArrayList<Integer> arr, ArrayList<Integer> ans) {
        
        if(index == n) {
            ans.add(sum);
            return;
        }
        
        subsum(index + 1, sum + arr.get(index), n, arr, ans);
        
        subsum(index + 1, sum, n, arr, ans);
        
        
    }
    
    ArrayList<Integer> subsetSums(ArrayList<Integer> arr, int n) {
        
        ArrayList<Integer> ans = new ArrayList<>();
        
        subsum(0, 0, n, arr, ans);
        
        return ans;
    }
}

```

## Complexity Analysis:

### Time Complexity: O(2^N) 

### Space Complexity: O(2^N)