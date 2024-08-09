# Boundary Traversal of Binary Tree

[Problem Link](https://www.naukri.com/code360/problems/boundary-traversal-of-binary-tree_790725)

![Image](https://files.codingninjas.in/boundarytraversal-5149.png)

## Approach - 1

1. This can be solved by three traversals, they are Left Bondary, Bottom Boundary and Right Boundary
2. First traverse the left Boundary (from root to the always left, if null, then right) and push the vlaue to the answer and not include the leaf node
3. Do any traversal and find the leaf nodes and push them to answer(Bottom traversal)
4. Traverse the right Boundary(from root to always to right, if null then left), use stack here to reverse the boundary, as we are traversing in anti-clock-wise direction

```c++

public class Solution {

    static void left(TreeNode root, List<Integer> ans) {
        if(root == null || (root.left == null && root.right == null)) return;

        ans.add(root.data);

        if(root.left != null) {
            left(root.left, ans);
        } else {
            left(root.right, ans);
        }
    }

    static void inorder(TreeNode root, List<Integer> ans) {
        if(root == null) return;

        inorder(root.left, ans);

        if(root.left == null && root.right == null) ans.add(root.data);

        inorder(root.right, ans);
    }

    static void right(TreeNode root, Stack<Integer> stack) {
        if(root == null || (root.left == null && root.right == null)) return;

        stack.push(root.data);

        if(root.right != null) {
            right(root.right, stack);
        } else {
            right(root.left, stack);
        }
    }

    public static List<Integer> traverseBoundary(TreeNode root){
        List<Integer> ans = new ArrayList<>();

        ans.add(root.data);

        left(root.left, ans);

        inorder(root, ans);

        Stack<Integer> stack = new Stack<>();

        right(root.right, stack);

        while(!stack.isEmpty()) {
            ans.add(stack.pop());
        }

        return ans;
    }
}

```

## Complexitiy Analysis:

### Time Complexity : O(N)

### Space Compleixty : O(N)
