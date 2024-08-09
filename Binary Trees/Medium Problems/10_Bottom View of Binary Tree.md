# Bottom View of Binary Tree

[Problem Link](https://www.geeksforgeeks.org/problems/bottom-view-of-binary-tree/1)

## Approach - 1

1. It is same as the `Top view of binary tree`
2. But in Top view, if we see the new column(vertical line) we only store that at first time
3. To get the bottom view, update it every time we see the column, the last modified are our answer
4. return the answer

```c++

class Solution {
  public:
    vector <int> bottomView(Node *root) {
        vector<int> ans;

        map<int, int> mp;
        queue<pair<Node *, int>> queue;

        queue.push({root, 0});

        while(!queue.empty()) {
            Node *curr = queue.front().first;
            int level = queue.front().second;
            queue.pop();

            mp[level] = curr->data;

            if(curr->left) queue.push({curr->left, level-1});
            if(curr->right) queue.push({curr->right, level+1});
        }

        for(auto &it : mp) {
            ans.push_back(it.second);
        }

        return ans;
    }
};

```

## Complexitiy Analysis:

### Time Complexity : O(N)

### Space Compleixty : O(N) + O(N)
