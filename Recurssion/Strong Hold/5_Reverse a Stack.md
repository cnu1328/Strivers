# Reverse a Stack


[Problem Link](https://www.geeksforgeeks.org/problems/reverse-a-stack/1)


## Approach - 1

1. Recurssively reverse the stack
2. The idea is that, remove all the elements from stack and call insertBottom funtion for every element.
3. the insertbottom function will pop's all the existing elements and pushes the new element to the last, and pushes again poped existing elements.



```Java

class Solution{
public:
    void insertBottom(stack<int> &st, int ele) {
        if(st.empty()) {
            st.push(ele);
            return;
        }
        
        int topele = st.top();
        st.pop();
        insertBottom(st, ele);
        st.push(topele);
        
    }

    void Reverse(stack<int> &st){
        if(st.empty())
            return;
        int ele = st.top();
        st.pop();
        Reverse(st);
        insertBottom(st, ele);
    }
};

```

## Complexity Analysis:

### Time Complexity: O(n^2) 

### Space Complexity: O(n)


## Approach - 2 - using queue

1. We can also take a help of a queue. 
2. We will extract the elements from stack one by one and keep inserting it in the queue. 
3. Once the stack becomes empty, we will start filling it by popping the elements from front end the queue

```Java

class Solution{
public:
    void Reverse(stack<int> &St){
        
    queue<int>q;
    while(!St.empty())
    {
        q.push(St.top());
        St.pop();
    }
    
    while(!q.empty())
    {
        St.push(q.front());
        q.pop();
    }
    
    }
};


```

## Complexity Analysis:

### Time Complexity: O(n) 

### Space Complexity: O(n)

