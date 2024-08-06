# Delete all occurrences of a given key in a doubly linked list

[Problem Link](https://www.geeksforgeeks.org/problems/delete-all-occurrences-of-a-given-key-in-a-doubly-linked-list/1)

## Approach - 1

1. First check and delete if the prefix nodes of linked list values are equal to the given key
2. After, Traverse the linked list from where you find the node value is not equal to the given key
3. Remove the node which have the value K, and attach the link between the prev and next node, if nodes exist
4. return the modified head node

```java

class Solution {
    static Node deleteAllOccurOfX(Node head, int x) {
        if(head == null) return null;

        Node temp = head;

        while(temp != null && temp.data == x) {
            temp = temp.next;
        }

        Node ansHead = temp;

        if(temp != null)
            temp.prev = null;

        while(temp != null) {

            if(temp.data == x) {
                Node prev = temp.prev;

                prev.next = temp.next;

                if(temp.next != null) {
                    temp.next.prev = prev;
                }
            }

            temp = temp.next;
        }

        return ansHead;
    }
}

```

## Complexity Analysis:

### Time Complexity: O(N)

### Space Complexity: (1)
