# Sort a stack

[Problem Link](https://www.geeksforgeeks.org/problems/sort-a-stack/1)

## Approach - Recurssion

1. First, store the stack top element in temp and remove top element from stack until stack become empty recurrsively
2. For every temp element, use insertedSort function to make the stack sorted, pass stack and temp element as arguments
3. in insertedSort function if stack is empty or the elemet is greater than stack top element then push the element to stack
4. else store top element in temp and call recursively insertedSort with same element
5. if this call finishes then push temp to stack

```Java

class GfG {
    
    private void insertStack(Stack<Integer> stack, int ele) {
        
        if(stack.isEmpty() || ele > stack.peek()) {
            stack.push(ele);
        }
        
        else {
            int temp = stack.pop();
            insertStack(stack, ele);
            stack.push(temp);
        }
    }
    
    private void sortStack(Stack<Integer> stack) {
        if(!stack.isEmpty()) {
            
            int temp = stack.pop();
            sortStack(stack);
            insertStack(stack, temp);
            
        }
    }
    
    public Stack<Integer> sort(Stack<Integer> s) {
        
        sortStack(s);
        
        return s;
    }
}


```

