# Prefix to Infix Conversion

[Problem Link](https://www.geeksforgeeks.org/problems/prefix-to-infix-conversion/1)

## Approach - 1

1. Traverse the string from last index
2. If a character is operand push it to the stack
3. If a character is operator then take top two stack elements and push them by combining with parententhesis
4. return the answer

```c++

class Solution {
  public:
    string preToInfix(string pre_exp) {

        stack<string> st;

        for(int i = pre_exp.length() - 1; i>=0; i--) {
            char c = pre_exp[i];

            if(c == '+' || c == '*' || c == '/' || c == '-') {

                string first = st.top();
                st.pop();
                string second = st.top();
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

### Time Complexity: O(N) +O(N)

### Space Complexity: (N)
