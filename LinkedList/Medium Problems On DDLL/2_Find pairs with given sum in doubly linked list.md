# Find pairs with given sum in doubly linked list

[Problem Link](https://www.geeksforgeeks.org/problems/find-pairs-with-given-sum-in-doubly-linked-list/1)

## Approach - 1

1. As the linked list is sorted, we can use low and high pointers
2. The sum of low.data and high.data if equal to given target then store this pair in answer list
3. The sum is less than target then move the low pointer to its next
4. The sum is greater than target then move high pointer to its prev
5. return the answer list

```Java

class Solution {
    public static ArrayList<ArrayList<Integer>> findPairsWithGivenSum(int target, Node head) {
        // code here
        ArrayList<ArrayList<Integer>> ans = new ArrayList<>();

        Node low = head;

        while(low.next != null) {
            low = low.next;
        }

        Node high = low;
        low = head;

        while(low.data < high.data) {
            ArrayList<Integer> pair = new ArrayList<>();

            int sum = low.data + high.data;


            if(sum == target) {
                pair.add(low.data);
                pair.add(high.data);

                ans.add(pair);

                low  = low.next;
                high = high.prev;
            }

            else if(sum < target) {
                low = low.next;
            } else {
                high = high.prev;
            }
        }

        return ans;

    }
}

```

## Complexity Analysis:

### Time Complexity: O(N)

### Space Complexity: (1)
