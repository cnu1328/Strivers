# Implement Stack using Linked List

[Problem Link](https://www.geeksforgeeks.org/problems/implement-stack-using-linked-list/1)

## Approach - 1

1. push - O(N)
2. pop - O(N)

```c++
#include <bits/stdc++.h>
using namespace std;

class Node {
public:
    int data;
    Node *next;
    
    Node(int _data) {
        data = _data;
        next = NULL;
    } 
};

class Stack {
public: 
    int size;
    Node *top;
    
    Stack() {
        size = 0;
        top = NULL;
    }
    
    void push(int ele) {
        Node *nn = new Node(ele);
        nn->next = top;
        top = nn;
        
        size ++;
    }
    
    int topEle() {
        if(top == NULL) return -1;
        
        return top->data;
    }
    
    void pop() {
        if(top) {
            top = top->next;
            size --;
        }
    }
    
    int stackSize() {
        return size;
    }
    
    bool empty() {
        return top == NULL;
    }
    
    
};

int main() {
    Stack st;
    
    st.push(10);
    st.push(20);
    st.push(30);
    st.push(40);
    st.push(50);
    cout<<st.topEle()<<endl;
    cout<<st.stackSize()<<endl;
    st.pop();
    cout<<st.topEle()<<endl;
    st.pop();
    cout<<st.empty()<<endl;
    cout<<st.topEle()<<endl;
    

}


```
