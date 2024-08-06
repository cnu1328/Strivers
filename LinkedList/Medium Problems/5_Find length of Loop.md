# Find length of Loop

[Problem Link](https://www.geeksforgeeks.org/problems/find-length-of-loop/1)

## Approach - 1

1. use slow and fast pointers
2. if slow == fast, then we have dectected a cycle
3. Then from slow, traverse to the next nodes, until slow == fast
4. Count every time
5. return the count

```Java

class Solution
{
    //Function to find the length of a loop in the linked list.
    static int countNodesinLoop(Node head)
    {
        Node slow = head;
        Node fast = head;

        while(fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;

            if(slow == fast) {
                int count = 1;

                slow = slow.next;

                while(slow != fast) {
                    count++;
                    slow = slow.next;
                }

                return count;

            }
        }

        return 0;
    }
}

```

## Complexity Analysis:

### Time Complexity: O(N)

### Space Complexity: (1)
