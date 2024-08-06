# Doubly linked list Insertion at given position

[Problem Link](https://www.geeksforgeeks.org/problems/insert-a-node-in-doubly-linked-list/1)

## Approach - 1

```c++
/*
struct Node
{
  int data;
  struct Node *next;
  struct Node *prev;
  Node(int x) { data = x; next = prev = NULL; }
}; */

//Function to insert a new node at given position in doubly linked list.
void addNode(Node *head, int pos, int data)
{
    Node *nn = new Node(data);
    Node *temp = head;


    for(int i=0; i<pos; i++) {
        temp = temp->next;
    }

   nn->prev = temp;
   nn->next = temp->next;
   temp->next = nn;

   if(nn->next != NULL) {
       nn->next->prev = nn;
   }
}

```

## Complexity Analysis:

### Time Complexity: O(pos)

### Space Complexity: (1)
