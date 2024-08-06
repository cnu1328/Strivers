# Introduction to Doubly Linked List

[Problem Link](https://www.geeksforgeeks.org/problems/introduction-to-doubly-linked-list/1)

## Approach - 1

```Java

/*
class Node{
public:
    Node* prev;
    int data;
    Node* next;

    Node()
    {
        prev = NULL;
        data = 0;
        next = NULL;
    }

    Node(int value)
    {
        prev = NULL;
        data = value;
        next = NULL;
    }
};*/

class Solution {
  public:
    Node* constructDLL(vector<int>& arr) {
        // code here

        Node *head = new Node(arr[0]);

        Node *tail = head;

        for(int i=1; i<arr.size(); i++) {
            Node *nn = new Node(arr[i]);

            tail->next = nn;
            nn->prev = tail;

            tail = nn;
        }

        return head;
    }
};


```

## Complexity Analysis:

### Time Complexity: O(N)

### Space Complexity: (1)
