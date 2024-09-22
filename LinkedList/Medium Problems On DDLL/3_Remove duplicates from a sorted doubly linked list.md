# Remove duplicates from a sorted doubly linked list

[Problem Link](https://www.geeksforgeeks.org/problems/remove-duplicates-from-a-sorted-doubly-linked-list/1)

## Approach - 1

1. First point at one node, then check its next node value is equal to the pointed node, if it is then check for its consecutive nodes until the node's value is not equal to the pointed node.
2. Do the same for other distinct nodes
3. return the head after modification

```java

class Solution{
    Node removeDuplicates(Node head){

        if(head == null || head.next == null) return head;

        Node curr = head;

        while(curr != null) {

            Node temp = curr;

            while(temp.next != null && temp.data == temp.next.data) {

                temp = temp.next;
            }

            if(temp == curr) {
                curr = curr.next;
            }

            else  {

                temp = temp.next;

                if(temp != null) {
                    curr.next = temp;
                    temp.prev = curr;
                } else {
                    curr.next = null;
                }

                curr = temp;

            }
        }

        return head;
    }
}
```

## Complexity Analysis:

### Time Complexity: O(N)

### Space Complexity: (1)


## Approach - 2

```c++

class Solution
{
public:

    Node * removeDuplicates(struct Node *head)
    {
        Node *curr = head->next;
        Node *removed = head;
        
        while(curr) {
            if(curr->data != removed->data) {
                removed->next = curr;
                curr->prev = removed;
                removed = curr;
            }
            
            curr = curr->next;
        }
        
        removed->next = NULL;
        
        return head;
    }
};

```

## Complexity Analysis:

### Time Complexity: O(N)

### Space Complexity: (1)
