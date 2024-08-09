# Unique Binary Tree Requirements

[Problem Link](https://www.geeksforgeeks.org/problems/unique-binary-tree-requirements/1)

## Approacch - 1

1. With pre-order and post-order we can't construct a unique binary tree
2. With Inorder and pre-order we can construct a unique binary tree
3. With Inorder and post-order we can construct a unique binary tree

```c++

class Solution{

    public static boolean isPossible(int a, int b){
        // Code here

        // preorder - 1
        // inorder - 2
        // postorder - 3

        if(((a == 2) && (b == 1 || b == 3)) ||
           ((b == 2) && (a == 1 || a == 3))) return true;

         return false;
    }
}

```

## Complexitiy Analysis:

### Time Complexity : O(1)

### Space Compleixty : O(1)
