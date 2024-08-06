# Plus-One-Linked-List

[Problem Link](https://www.geeksforgeeks.org/add-1-number-represented-linked-list/)

## Approach - 1

1. First reverse the given linked list
2. Sum the the first node of reversed list by 1, modify its the node's data
3. send the carray to the next node
4. reverse the node

```C++

static Node reverse(Node head)
{
    Node prev = null;
    Node current = head;
    Node next = null;
    while (current != null) {
        next = current.next;
        current.next = prev;
        prev = current;
        current = next;
    }
    return prev;
}

/* Adds one to a linked lists and return the head
node of resultant list */
static Node addOneUtil(Node head)
{
    // res is head node of the resultant list
    Node res = head;
    Node temp = null, prev = null;

    int carry = 1, sum;

    while (head != null) // while both lists exist
    {
        // Calculate value of next digit in resultant
        // list. The next digit is sum of following
        // things (i) Carry (ii) Next digit of head list
        // (if there is a next digit)
        sum = carry + head.data;

        // update carry for next calculation
        carry = (sum >= 10) ? 1 : 0;

        // update sum if it is greater than 10
        sum = sum % 10;

        // Create a new node with sum as data
        head.data = sum;

        // Move head and second pointers to next nodes
        temp = head;
        head = head.next;
    }

    // if some carry is still there, add a new node to
    // result list.
    if (carry > 0)
        temp.next = newNode(carry);

    // return head of the resultant list
    return res;
}

// This function mainly uses addOneUtil().
static Node addOne(Node head)
{
    // Reverse linked list
    head = reverse(head);

    // Add one from left to right of reversed
    // list
    head = addOneUtil(head);

    // Reverse the modified list
    return reverse(head);
}

```

## Complexity Analysis:

### Time Complexity: O(N)

### Space Complexity: (1)
