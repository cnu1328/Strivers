# Binary Tree Representation

[Problem Link](https://www.geeksforgeeks.org/problems/binary-tree-representation/1)

## Approach - 1

![image](https://github.com/user-attachments/assets/49867937-39f9-485a-82e3-fd09e32a30b5)

1. To insert a node to a tree,
2. Traverse the tree in level order and when ever you find the curr->left equal to null then assign value to it and curr->right equal to null then assign value
3. If not push the curr node to queue

```c++

class Solution{
public:

   node* insert(node *root, int val) {

       if(root == NULL) {
           return newNode(val);
       }

       queue<node *> que;
       que.push(root);

       while(!que.empty()) {

           node *curr = que.front();
           que.pop();

           if(curr->left == NULL) {
               curr->left = newNode(val);
               break;
           } else {
               que.push(curr->left);
           }

           if(curr->right == NULL) {
               curr->right =  newNode(val);
               break;
           } else {
               que.push(curr->right);
           }
       }

       return root;
   }


    void create_tree(node* root0, vector<int> &vec){

        for(int i=1; i<vec.size(); i++) {
            root0 = insert(root0, vec[i]);
        }

    }

};

```

## Complexitiy Analysis:

### Time Complexity : O(N)

### Space Compleixty : O(N)
