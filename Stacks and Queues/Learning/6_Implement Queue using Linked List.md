# Implement Queue using Linked List

[Problem Link](https://www.geeksforgeeks.org/problems/implement-queue-using-linked-list/1)

## Approach - 1

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

class Queue {
    int size;
    Node *front, *rear;
public:   
    Queue() {
        size = 0;
        front = rear = NULL;
    }
    
    void push(int ele) {
        if(front == NULL) {
            front = new Node(ele);
            rear = front;
        }
        
        else {
            rear->next = new Node(ele);
            rear = rear->next;
        }
        
        size ++;
    }
    
    int top() {
        if(front) {
            return front->data;
        }
    }
    
    void pop() {
        if(front) {
            front = front->next;
            
            size --;
        }
    }
    
    int queSize() {
        return size;
    }
    
    bool empty() {
        return front == NULL;
    }
};

int main() {
	Queue que;
	
	que.push(10);
	que.push(20);
	que.push(30);
	que.push(40);
	que.push(50);
	
	cout<<que.top()<<endl;
	que.pop();
	cout<<que.top()<<endl;
	que.pop();
	cout<<que.queSize()<<endl;
	que.pop();
	cout<<que.empty()<<endl;
	

}


```
