# Delete node in Doubly Linked List

[Problem Link](https://www.geeksforgeeks.org/problems/delete-node-in-doubly-linked-list/1)

## Approach - 1

```Java

/*

Definition for doubly Link List Node
class Node
{
    int data;
    Node next;
    Node prev;
    Node(int x){
        data = x;
        next = null;
        prev = null;
    }
}
*/
class Solution {
    public Node deleteNode(Node head, int x) {

        if(x == 1) {
            head = head.next;
            head.prev = null;
            return head;
        }

        int cnt = 1;

        Node temp = head;

        while(cnt < x) {
            cnt++;
            temp = temp.next;
        }

        temp.prev.next = temp.next;

        if(temp.next != null) {
            temp.next.prev = temp.prev;
        }

        return head;

    }
}

```

## Complexity Analysis:

### Time Complexity: O(X)

### Space Complexity: (1)
