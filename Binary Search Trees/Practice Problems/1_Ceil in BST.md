# Ceil in BST

[Problem Link](https://www.geeksforgeeks.org/problems/implementing-ceil-in-bst/1)

## Approach - 1

1. The ceil is nothing but, find the equal or immediate grater element for the given key
2. The idea is if we find the key value in the tree then return the value
3. Or else, if the key value is greater than curr node value, It means current node value is less than the key value. so we don't require this node, just move curr->right to get bigger values
4. or else if the key value is less than curr node value, then the curr node value is might be our answer, so update the ceil
5. return the ceil

```c++

int findCeil(Node* root, int key) {
    if (root == NULL) return -1;

    int ciel = -1;

    Node *curr = root;

    while(curr) {

        if(curr->data == key) return curr->data;

        if(key < curr->data) {
            ciel = curr->data;
            curr = curr->left;
        }

        else {
            curr = curr->right;
        }
    }

    return ciel;
}

```

## Complexitiy Analysis:

### Time Complexity : O(H)

### Space Compleixty : O(H)
