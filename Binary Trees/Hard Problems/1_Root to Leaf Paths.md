# Root to Leaf Paths

[Problem Link](https://www.geeksforgeeks.org/problems/root-to-leaf-paths/1)

## Approach - 1

1. Perform the pre-order traversal
2. before calling the left-subtree, add the currnode value to the current array
3. Check if the currnode is a leaf tree, if it is then push curr to the answer
4. call left sub-tree
5. call right sub-tree
6. remove the last value from current array

```c++

class Solution {
  public:
    void preorder(Node *root, vector<int> &curr, vector<vector<int>> &ans) {
        if(root == nullptr) {
            return;
        }

        curr.push_back(root->data);

        if(root->left == nullptr && root->right == nullptr)
            ans.push_back(curr);

        preorder(root->left, curr, ans);
        preorder(root->right, curr, ans);

        curr.pop_back();
    }

    vector<vector<int>> Paths(Node* root) {
        // code here

        vector<vector<int>> ans;
        vector<int> curr;

        preorder(root, curr, ans);

        return ans;
    }
};

```

## Complexitiy Analysis:

### Time Complexity : O(N)

### Space Compleixty : O(H)
