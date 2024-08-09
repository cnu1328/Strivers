# Postfix to Infix Conversion

[Problem Link](https://www.geeksforgeeks.org/problems/postfix-to-infix-conversion/1)

## Approach - 1

1. When you find a operand then push to the stack
2. When a current character is operator then take two operands from the stack and append them with the stack

```c++

class Solution {
  public:
    string postToInfix(string exp) {

        string ans = "";

        stack<string> st;

        for(char c : exp) {
            if(c == '*' || c == '+' || c == '-' || c == '/') {

                string second = st.top();
                st.pop();
                string first = st.top();
                st.pop();

                st.push('(' + first + c + second + ')');

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
