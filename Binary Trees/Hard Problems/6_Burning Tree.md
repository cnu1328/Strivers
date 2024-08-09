# Burning Tree

[Problem Link](https://www.geeksforgeeks.org/problems/burning-tree/1)

## Approach - 1

1. First make connections for every child to its parent, so we can easily access the a child parent.
2. Do it with the help of queue(level order traversal)
3. After building the parent connection
4. Do level order traversal again
5. Find the target node in the tree
6. Do level order traversal and at every level increemnt ans
7. return the answer

```c++

class Solution {
  public:

    Node * findNode(Node *root, int target) {
        if(root == NULL) return NULL;

        if(root->data == target) return root;

        Node *left =  findNode(root->left, target);
        Node *right = findNode(root->right, target);

        if(left) return left;

        if(right) return right;

        return NULL;
    }

    void makeParent(Node *root, unordered_map<Node *, Node *> &parent) {

        queue<Node *> que;

        que.push(root);

        while(!que.empty()) {
            int n = que.size();

            for(int i=0; i<n; i++) {
                Node *curr = que.front();
                que.pop();

                if(curr->left) {
                    parent[curr->left] = curr;
                    que.push(curr->left);
                }

                if(curr->right) {
                    parent[curr->right] = curr;
                    que.push(curr->right);
                }
            }
        }
    }

    int minTime(Node* root, int target)
    {
        unordered_map<Node *, Node *> parent;

        makeParent(root, parent);

        unordered_map<Node *, bool> visited;

        queue<Node *> que;

        Node *targetNode = findNode(root, target);

        que.push(targetNode);
        visited[targetNode] = 1;

        int sec = 0;

        while(!que.empty()) {
            int n = que.size();
            sec ++;

            for(int i=0; i<n; i++) {
                Node *curr = que.front();
                que.pop();

                if(curr->left && !visited[curr->left]) {
                    visited[curr->left] = 1;
                    que.push(curr->left);
                }

                if(curr->right && !visited[curr->right]) {
                    visited[curr->right] = 1;
                    que.push(curr->right);
                }

                if(parent[curr] && !visited[parent[curr]]) {
                    visited[parent[curr]] = 1;
                    que.push(parent[curr]);
                }
            }
        }

        return sec > 0 ? sec - 1 : sec;
    }
};

```

## Complexitiy Analysis:

### Time Complexity : O(N)

### Space Compleixty : O(N)
