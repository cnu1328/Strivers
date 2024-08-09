# Minimum element in BST

[Problem Link](https://www.geeksforgeeks.org/problems/minimum-element-in-bst/1)

## Approach - 1 - Brute Force Approach

1. Traverse the entire tree and find the minimum / maximum element

```c++

class Solution {
    int res=0,mini=INT_MAX;
    public:
    void helper(Node* root){

        if(root==NULL)
        return ;

        helper(root->left);
        mini=min(mini,root->data);
        helper(root->right);

    }
  public:
    int minValue(Node* root) {
        // Code here
        helper(root);
        return mini;
    }
};

```

## Complexitiy Analysis:

### Time Complexity : O(N)

### Space Compleixty : O(N)

## Approach - 2 - Optimal Approach

1. To find the minimum element, just traverse always left side from root node till node->left null
2. To find the maximum element, just traverse always right side from root node till node ->right null

## Complexitiy Analysis:

### Time Complexity : O(Log<sub>2</sub>N)

### Space Compleixty : O(Log<sub>2</sub>N)
