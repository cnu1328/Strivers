# Children Sum in a Binary Tree

[Problem Link](https://www.geeksforgeeks.org/problems/children-sum-parent/1)

## Approach - 1

1. The idea is to traverse the tree in post order fashion.
2. if the node is null return true
3. if the node is leaf then return true
4. call function on left sub-tree as left
5. call function on right sub-tree as right
6. If any call return false then return false from here
7. sum = 0,
8. sum from its children and check with the root value, if equal return true else return false

```c++

class Solution{
    public:

    int isSum(Node *root) {
        if(root == NULL) return 1;

        if(root->left == NULL && root->right == NULL) return 1;

        int left = isSum(root->left);
        int right = isSum(root->right);

        if(left == false || right == false) return false;

        int sum = 0;

        if(root->left != NULL) sum += root->left->data;
        if(root->right != NULL) sum += root->right->data;

        if(sum == root->data) return true;

        return false;
    }

    int isSumProperty(Node *root) {
        return isSum(root);
    }
};

```

## Complexitiy Analysis:

### Time Complexity : O(N)

### Space Compleixty : O(H)
