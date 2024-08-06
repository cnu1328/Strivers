# Linked List Insertion At End

[Problem Link](https://www.geeksforgeeks.org/problems/linked-list-insertion-1587115620/0)

## Approach - 1

1. Traverse the linked list to last node and attach new node to it

```Java

class Solution {
  public:
    Node *insertAtEnd(Node *head, int x) {
        // Code here

        if(head == NULL) {
            return new Node(x);
        }

        Node *temp = head;

        while(temp->next != NULL) {
            temp = temp->next;
        }

        temp->next = new Node(x);

        return head;
    }
};


```

## Complexity Analysis:

### Time Complexity: O(N)

### Space Complexity: (1)
