# Flattening a Linked List

[Problem Link](https://www.geeksforgeeks.org/problems/flattening-a-linked-list/1)

## Approach - 1

1. Traverse the entire linked list and store all nodes in array
2. Sort the array
3. Construct the tree with array values

<img width="790" alt="image" src="https://github.com/user-attachments/assets/29c9c77b-4a74-41aa-9b76-e062553aaf6b">

```c++


class Solution {
  public:

    void getAllValues(Node *root, vector<int> &arr) {
        if(root == NULL) return;

        Node *curr = root;

        while(curr) {
            Node *child = curr->bottom;
            arr.push_back(curr->data);

            while(child) {
                arr.push_back(child->data);
                child = child->bottom;
            }

            curr = curr->next;

        }
    }

    Node *constructFlatten(vector<int> &arr) {

        if(arr.size() == 0) return NULL;


        Node *head = new Node(arr[0]);
        Node *tail = head;

        for(int i=1; i<arr.size(); i++) {

            tail->bottom = new Node(arr[i]);
            tail = tail->bottom;
        }

        return head;
    }

    Node *flatten(Node *root) {
        vector<int> arr;

        getAllValues(root, arr);

        sort(arr.begin(), arr.end());

        return constructFlatten(arr);
    }
};

```

## Complexitiy Analysis:

### Time Complexity : O(2 \* (M \* N)) + O( X Log X) => X = M \* N

### Space Compleixty : O(2 \* (M \* N))

## Approach - 2

1. First Know how to merge two sorted lists to one list
2. Then, from the given list, every time take two lists, and merge them,
3. And take one merged list and next list and merge them, continue till merge all the lists into one

<img width="801" alt="image" src="https://github.com/user-attachments/assets/ccbeca5e-176f-4a4c-9900-fd63c1f1d504">

```c++


class Solution {
  public:

    Node *merge(Node *p, Node *q) {
        Node *dummy = new Node(-1);
        Node *tail = dummy;

        while(p && q) {
            if(p->data <= q->data) {
                tail->bottom = p;
                p = p->bottom;
            }

            else {
                tail->bottom = q;
                q = q->bottom;
            }

            tail = tail->bottom;
        }

        if(p) {
            tail->bottom = p;
        }

        if(q) {
            tail->bottom = q;
        }

        return dummy->bottom;

    }

    Node *flatten(Node *root) {
        if(root == NULL || root->next == NULL) return root;

        Node *p = root;

        root = root->next;

        p->next = NULL;

        Node *head, *next;

        while(root) {

            next = root->next;

            root->next = NULL;

            p = merge(p, root);

            root = next;
        }

        return p;
    }
};

```

## Complexitiy Analysis:

### Time Complexity : O(2 \* M \* N)

### Space Compleixty : O(1)
