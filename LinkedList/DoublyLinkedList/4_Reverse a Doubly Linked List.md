# Reverse a Doubly Linked List

[Problem Link](https://www.geeksforgeeks.org/problems/reverse-a-doubly-linked-list/1)

## Approach - 1

```c++

/*
struct Node
{
    int data;
    Node * next;
    Node * prev;
    Node (int x)
    {
        data=x;
        next=NULL;
        prev=NULL;
    }

};
*/
Node* reverseDLL(Node * head)
{
    if(head == NULL)
        return NULL;

    Node *curr = head, *prev = NULL, *next = NULL;

    while(curr != NULL) {
        next = curr->next;
        curr->next = prev;
        curr->prev = next;


        prev = curr;
        curr = next;
    }

    return prev;

}

```

## Complexity Analysis:

### Time Complexity: O(N)

### Space Complexity: (1)
