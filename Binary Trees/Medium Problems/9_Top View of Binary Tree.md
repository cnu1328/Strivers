# Top View of Binary Tree

[Problem Link](https://www.geeksforgeeks.org/problems/top-view-of-binary-tree/1)

## Approach - 1

1. If we view the tree from top, then all the shadowed nodes will not visible and all other nodes will visible
2. To solve this problem use the concept of vertical and level order traversal
3. If we see the vertical line for the first time, then only store the respective node, which specifies that, this node is the first node on that vertical line, which is visible from top
4. Perform level order traversal, if we go left then do (col - 1) and if we go right (col + 1)
5. return the answer

```c++

class Solution
{
    public:
    //Function to return a list of nodes visible from the top view
    //from left to right in Binary Tree.
    vector<int> topView(Node *root)
    {
        vector<int> ans;
        map<int, Node *> nodes;
        queue<pair<Node *, int>> queue;

        queue.push({root, 0});

        while(!queue.empty()) {
            auto pr = queue.front();
            Node *curr = pr.first;
            int line = pr.second;
            queue.pop();

            if(nodes.find(line) == nodes.end()) {
                nodes[line] = curr;
            }

            if(curr->left) queue.push({curr->left, line-1});
            if(curr->right) queue.push({curr->right, line+1});

        }

        for(auto &it : nodes) {
            ans.push_back(it.second->data);
        }

        return ans;
    }

};


```

## Complexitiy Analysis:

### Time Complexity : O(N)

### Space Compleixty : O(N) + O(N)
