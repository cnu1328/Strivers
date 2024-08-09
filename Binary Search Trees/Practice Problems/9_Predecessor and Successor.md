# Predecessor and Successor

[Problem Link](https://www.geeksforgeeks.org/problems/predecessor-and-successor/1)

## Approach - 1

1. The given key element will present in the tree or not
2. The main objective here is that, finding the predecessor and successor for the given key
3. For a key, the predecessor is the immediate smallest value of key value
4. For a key, the successor is the immediate largest value of key value

```c++

class Solution
{
    public:
    void findPreSuc(Node* root, Node*& pre, Node*& suc, int key)
    {
        pre = NULL;
        suc = NULL;

        Node *curr = root;

        while(curr) {
            if(curr->key >= key) {
                curr = curr->left;
            } else {
                pre = curr;
                curr = curr->right;
            }
        }

        curr = root;

        while(curr) {
            if(curr->key <= key) {
                curr = curr->right;
            }

            else {
                suc = curr;
                curr = curr->left;
            }
        }
    }
};

```

## Complexitiy Analysis:

### Time Complexity : O(H)

### Space Compleixty : O(1)
