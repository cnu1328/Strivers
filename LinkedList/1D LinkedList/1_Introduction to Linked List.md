# Introduction to Linked List

[Problem Link](https://www.geeksforgeeks.org/problems/introduction-to-linked-list/1)

## Approach - 1

1. Traverse the array, and create new nodes and attarch to the end of linked list

```Java

/*class Node {
public:
    int data;
    Node* next;

    // Default constructor
    Node()
    {
        data = 0;
        next = NULL;
    }

    // Parameterised Constructor
    Node(int data)
    {
        this->data = data;
        this->next = NULL;
    }
};*/

class Solution {
  public:
    Node* constructLL(vector<int>& arr) {
        Node * head = new Node(arr[0]);
        Node *tail = head;

        for(int i=1; i<arr.size(); i++) {
            tail->next = new Node(arr[i]);
            tail = tail->next;
        }

        return head;

    }
};

```

## Complexity Analysis:

### Time Complexity: O(N)

### Space Complexity: (1)
