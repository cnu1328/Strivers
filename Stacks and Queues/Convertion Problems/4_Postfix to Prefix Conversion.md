# Postfix to Prefix Conversion

[Problem Link](https://www.geeksforgeeks.org/problems/postfix-to-prefix-conversion/1)

## Approach - 1

1. Traverse the string from first
2. If a character is operator, then take top two strings and push like ( c + first + second)
3. If a character is operand, then push it into the stack
4. return the top stack element

```c++

class Solution {
  public:
    string postToPre(string post) {
        // Write your code here

        stack<string> st;

        for(char c : post) {
            if(c == '+' || c == '*' || c == '/' || c == '-') {

                string second = st.top();
                st.pop();
                string first = st.top();
                st.pop();

                st.push(c + first + second);

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
