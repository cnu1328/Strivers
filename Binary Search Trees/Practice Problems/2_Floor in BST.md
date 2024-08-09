# Floor in BST

[Problem Link](https://www.geeksforgeeks.org/problems/floor-in-bst/1)

## Approach - 1

1. The floor is nothing but, find the equal or immediate smaller element for the given key
2. The idea is if we find the key value in the tree then return the value
3. Or else, if the key value is greater than curr node value, It means current node value is less than the key value. So, the curr node value is might be our answer, so update the floor
4. or else if the key value is less than curr node value, so we don't require the right branch, curr = curr->left
5. return the ceil

```c++

class Solution{

public:
    int floor(Node* root, int key) {

        if(root == NULL) return -1;

        int flor = -1;

        Node *curr = root;

        while(curr) {

            if(curr->data == key) return key;

            if(key > curr->data) {
                flor = curr->data;
                curr = curr->right;
            }

            else {
                curr = curr->left;
            }
        }

        return flor;
    }
};

```

## Complexitiy Analysis:

### Time Complexity : O(H)

### Space Compleixty : O(H)
