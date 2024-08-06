# Count Linked List Nodes

[Problem Link](https://www.geeksforgeeks.org/problems/count-nodes-of-linked-list/0)

## Approach - 1

1. Traverse the list and count the nodes

```Java

/* Link list node */
/*
struct Node
{
    int data;
    Node* next;
    Node(int x) {  data = x;  next = NULL; }
}; */

class Solution {
  public:
    // Function to count nodes of a linked list.
    int getCount(struct Node* head) {

        int count = 0;

        Node *temp = head;

        while(temp != NULL) {
            temp = temp->next;
            count++;
        }

        return count;
    }
};


```

## Complexity Analysis:

### Time Complexity: O(N)

### Space Complexity: (1)
