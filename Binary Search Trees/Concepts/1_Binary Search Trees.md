# Binary Search Trees

[Problem Link](https://www.geeksforgeeks.org/problems/binary-search-trees/1)

**Binary Search Trees**, popularly known as BST, are the category of Binary Trees used to optimize the operation of searching an element among the Tree Nodes in a Binary Tree.

![image](https://github.com/user-attachments/assets/686cde57-ea06-4635-97ce-526d0a69390d)

**For every Binary Search if left and right sub-tree exist, then**

```txt

Left Child < Node < Right Child

```

1. In BST, the maximum height in almost all cases is kept in order of **log(N)2**
2. Binary Tree whose maximum height can reach the order of **N** when the tree is **skewed**.

**The Binary Search Trees, inorder traversal gives us sorted (ascending) order.**

## All Operations on Binary Search Trees

```java

#include <bits/stdc++.h>
using namespace std;

class TreeNode {
 public:
    int data;
    TreeNode *left;
    TreeNode *right;
    
    TreeNode(int val) {
        data = val;
        left = right = NULL;
    }
};

TreeNode * insertToBST(TreeNode *root, int key) {
    
    if(!root) 
        return new TreeNode(key);
    
    
    TreeNode *curr = root;
    
    while(curr) {
        if(key < curr->data) {
            if(curr->left) {
                curr = curr->left;
            }
            
            else {
                curr->left = new TreeNode(key);
                break;
            }
        }
        
        else {
            if(curr->right) {
                curr = curr->right;
            }
            
            else {
                curr->right = new TreeNode(key);
                break;
            }
        }
    }
    
    return root;
}

TreeNode *constructBST(vector<int> arr) {
    
    TreeNode *root = NULL;
    
    for(int i=0; i<arr.size(); i++) {
        root = insertToBST(root, arr[i]);
    }
    
    return root;
}

void inorder(TreeNode *root) {
    if(!root) return;
    
    inorder(root->left);
    cout<<root->data<<" ";
    inorder(root->right);
}

bool search(TreeNode * root, int key) {
    if(!root) return root;
    
    TreeNode *curr = root;
    
    while(curr) {
        if(key == curr->data) {
            return true;
        }
        
        else if(key < curr->data) {
            curr = curr->left;
        }
        
        else {
            curr = curr->right;
        }
    }
    
    return false;
}

TreeNode* findPre(TreeNode *root) {
    if(!root->right) return root;
    
    return findPre(root->right);
}

TreeNode *performDelete(TreeNode *root) {
    if(!root->left) return root->right;
    
    else if(!root->right) return root->left;
    
    else {
        TreeNode *pre = findPre(root->left);
        
        pre->right = root->right;
        
        return root->left;
    }
}

TreeNode *deleteNode(TreeNode *root, int key) {
    if(!root) return root;
    
    if(root->data == key) {
        return performDelete(root);
    }
    
    TreeNode*curr = root;
    
    while(curr) {
        if(key < curr->data) {
            if(curr->left && curr->left->data == key) {
                curr->left = performDelete(curr->left);
            }
            
            else {
                curr = curr->left;
            }
        }
        
        else {
            if(curr->right && curr->right->data == key) {
                curr->right = performDelete(curr->right);
            } else {
                curr = curr->right;
            }
        }
    }
    
    return root;
    
    
}

int main() {
	
	int n;
	cin>>n;
	
	vector<int> arr(n);
	
	for(int i=0; i<n; i++) {
	    cin>>arr[i];
	}
	
	TreeNode *root = constructBST(arr);
	
	inorder(root);
    
    bool found = search(root, -1);
    
    cout<<endl;
    if(found) cout<<"Found"<<endl;
    else cout<<"NOT Found"<<endl;
    
    root = deleteNode(root, 6);
    
    inorder(root);
}


```
