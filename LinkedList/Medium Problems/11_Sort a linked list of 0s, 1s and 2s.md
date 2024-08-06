# Sort a linked list of 0s, 1s and 2s

[Problem Link](https://www.geeksforgeeks.org/problems/given-a-linked-list-of-0s-1s-and-2s-sort-it/1)

## Approach - 1

1. Declare an array, and push all the elements to the array
2. sort the array using (low, mid and high) pointers
3. Replace the array elements to the linked list
4. return the linked list

## Complexity Analysis:

### Time Complexity: O(N)

### Space Complexity: (N)

## Approach - 2

1. Count the number of zero's, one's and two's
2. Replace the zero number of times in the beginning of list, and then one and then two's
3. return the head

```Java

class Solution
{
    public:
    Node* segregate(Node *head) {

        Node *temp = head;

        int zero = 0, one = 0, two = 0;

        while(temp != NULL) {
            if(temp->data == 0)
                zero++;
            else if(temp->data == 1)
                one++;
            else
                two++;
            temp = temp->next;
        }

        temp = head;

        while(temp != NULL) {
            if(zero != 0) {
                temp->data = 0;
                zero--;
            }

            else if(one != 0) {
                temp->data = 1;
                one--;
            }

            else if(two != 0) {
                temp->data = 2;
                two--;
            }

            temp = temp->next;
        }

        return head;
    }
};

```

## Complexity Analysis:

### Time Complexity: O(N)

### Space Complexity: (1)

## Approach - 3 - use 0, 1, 2 pointers

1. Declare three pointers(0, 1, 2)
2. Traverse the Linked list
3. If you find the node with value 0, then attach it to zero' pointer
4. If you find the node with value 1, then attach it to one's pointer
5. If you find the node with value 2, then attach it to two's pointer
6. return the zero next pointer

```java

//Back-end complete function Template for Java

class Solution {
    // Function to sort a linked list of 0s, 1s and 2s.
    static Node segregate(Node head) {
        if (head == null || head.next == null) return head;

        // creating three dummy nodes to point to beginning of the linked lists.
        Node zeroD = new Node(0);
        Node oneD = new Node(0);
        Node twoD = new Node(0);

        // initializing current pointers for three lists.
        Node zero = zeroD, one = oneD, two = twoD;
        Node curr = head;

        // traversing over the list with a pointer.
        while (curr != null) {
            // we check data at current node and store the node in it's
            // respective list and update the link part of that list.
            if (curr.data == 0) {
                zero.next = curr;
                zero = zero.next;
            } else if (curr.data == 1) {
                one.next = curr;
                one = one.next;
            } else {
                two.next = curr;
                two = two.next;
            }

                curr = curr.next;

        }
        // attaching the three lists containing 0s,1s and 2s respectively.
        zero.next = (oneD.next != null) ? (oneD.next) : (twoD.next);
        one.next = twoD.next;
        two.next = null;

        // updating the head of the list.
        head = zeroD.next;
        return head;
    }
}

```

## Complexity Analysis:

### Time Complexity: O(N)

### Space Complexity: (1)
