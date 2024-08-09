# Prefix to Postfix Conversion

[Problem Link](https://www.geeksforgeeks.org/problems/prefix-to-postfix-conversion/1)

## Approach - 1

1. Traverse the string from last index
2. if character is operator, then take top two elements from stack and push to the stack
   (first + second + c)
3. if a character is operand, then push to the stack
4. return the stack top element

```c++

class Solution {
  public:
    string preToPost(string pre) {

        stack<string> st;

        for(int i=pre.length() - 1; i>=0; i--) {

            char c = pre[i];

            if(c == '+' || c == '/' || c == '*' || c == '-') {
                string first = st.top();
                st.pop();
                string second = st.top();
                st.pop();

                st.push(first + second + c);
            } else {
                st.push(string(1, c));
            }
        }

        return st.top();
    }
};

```

## Complexity Analysis:

### Time Complexity: O(N) + O(N)

### Space Complexity: (N)
