# Search in Linked List

[Problem Link](https://www.geeksforgeeks.org/problems/search-in-linked-list-1664434326/1)

## Approach - 1

1. Traverse and search for it

```Java

struct Node
{
    int data;
    Node* next;
    Node(int x) {  data = x;  next = NULL; }
}; */

class Solution {
  public:
    // Function to count nodes of a linked list.
    bool searchKey(int n, struct Node* head, int key) {


        Node *temp = head;

        while(temp != NULL) {

            if(temp->data == key) return true;
            temp = temp->next;

        }

        return false;
    }
};

```

## Complexity Analysis:

### Time Complexity: O(N)

### Space Complexity: (1)
