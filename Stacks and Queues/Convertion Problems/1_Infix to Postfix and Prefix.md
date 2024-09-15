# Infix to Postfix

[Problem Link](https://www.geeksforgeeks.org/problems/infix-to-postfix-1587115620/1)

## Approach - 1

<img width="782" alt="image" src="https://github.com/user-attachments/assets/47a6c611-288e-4a96-bd1c-69560e97de2a">

```c++

#include<bits/stdc++.h>

using namespace std;

//Function to return precedence of operators
int prec(char c) {
  if (c == '^')
    return 3;
  else if (c == '/' || c == '*')
    return 2;
  else if (c == '+' || c == '-')
    return 1;
  else
    return -1;
}

// The main function to convert infix expression
//to postfix expression
void infixToPostfix(string s) {

  stack < char > st; //For stack operations, we are using C++ built in stack
  string result;

  for (int i = 0; i < s.length(); i++) {
    char c = s[i];

    // If the scanned character is
    // an operand, add it to output string.
    if ((c >= 'a' && c <= 'z') || (c >= 'A' && c <= 'Z') || (c >= '0' && c <= '9'))
      result += c;

    // If the scanned character is an
    // ‘(‘, push it to the stack.
    else if (c == '(')
      st.push('(');

    // If the scanned character is an ‘)’,
    // pop and to output string from the stack
    // until an ‘(‘ is encountered.
    else if (c == ')') {
      while (st.top() != '(') {
        result += st.top();
        st.pop();
      }
      st.pop();
    }

    //If an operator is scanned
    else {
      while (!st.empty() && prec(s[i]) <= prec(st.top())) {
        result += st.top();
        st.pop();
      }
      st.push(c);
    }
  }

  // Pop all the remaining elements from the stack
  while (!st.empty()) {
    result += st.top();
    st.pop();
  }

  cout << "Prefix expression: " << result << endl;
}

int main() {
  string exp = "(p+q)*(m-n)";
  cout << "Infix expression: " << exp << endl;
  infixToPostfix(exp);
  return 0;
}

```

## Complexity Analysis:

### Time Complexity: O(N)

### Space Complexity: (N)

# Inix to Prefix

## Approach - 1

1. First reverse the given string
2. In reversed string, take care of brackets
3. Perform Infix to postfix with controlled(i.e, precedence[s[i]] < precedence[st.top()])
4. Reverse the resultant
5. return the resultant string

```c++

#include <bits/stdc++.h>
using namespace std;

int pre(char c) {
    if(c == '^') return 3;
    
    else if(c == '/' || c == '*') return 2;
    
    else if(c == '+' || c == '-') return 1;
    
    return -1;
}

string convertToPostFix(string str) {
    stack<char> st;
    string ans = "";
    string num = "";
    int n = str.length();
    
    for(int i=0; i<str.length(); i++) {
        char c = str[i];
        
        if(c >= '1' && c <= '9') {
            
            while(i < n && isdigit(str[i])) {
                num += str[i];
                i++;
            }
            
            i--;
            
            ans += num + "#";
            num = "";
        }
        
        else if(c == '(') {
            st.push(c);
        }
        
        else if(c == ')') {
            while(st.top() != '(') {
                ans += st.top();
                st.pop();
            }
            
            st.pop();
        }
        
        else {
            while(!st.empty() && pre(c) <= pre(st.top())) {
                ans += st.top();
                st.pop();
            }
            
            st.push(c);
        }
    
    }
    
    while(!st.empty()) {
        ans += st.top();
        st.pop();
    }
    
    return ans;
    
}

int getVal(string post) {
    
    stack<int> st;
    int n = post.length();
    
    for(int i=0; i<n; i++) {
        char c = post[i];
        
        if(isdigit(c)) {
            int num = 0;
            
            while(i < n && isdigit(post[i])) {
                num = num * 10 + post[i] - '0';
                i++;
            }
            
            st.push(num);
        }
        
        else {
            int second = st.top();
            st.pop();
            int first = st.top();
            st.pop();
            
            if(c == '^') {
                st.push(pow(first, second));
            }
            
            else if(c == '*') {
                st.push(first * second);
            }
            
            else if(c == '/') {
                st.push(first / second);
            }
            
            else if(c == '+') {
                st.push(first + second);
            }
            
            else if(c == '-') {
                st.push(first - second);
            }
        }
        
        
    }
    
    return st.top();
    
    
}

string convertToPrefix(string str) {
    reverse(str.begin(), str.end());
    // ")3-1^55(*3+452"
    
    int n = str.length();
    string ans = "";
    stack<char> st;
    
    for(int i=0; i<n; i++) {
        char c = str[i];
        if(isdigit(c)) {
            string num = "";
            
            while(i < n && isdigit(str[i])) {
                num += str[i];
                i++;
            }
            
            i--;
            
            reverse(num.begin(), num.end());
            
            ans += num + "#";
        }
        
        else if(c == ')') {
            st.push(c);
        }
        
        else if(c == '(') {
            while(st.top() != ')') {
                ans += st.top();
                st.pop();
            }
            st.pop();
        }
        
        else {
            while(!st.empty() && pre(c) < pre(st.top())) {
                ans += st.top();
                st.pop();
            }
            
            st.push(c);
        }
    }
    
    while(!st.empty()) {
        ans += st.top();
        st.pop();
    }
    
    reverse(ans.begin(), ans.end());
    
    return ans;
    
}

int getPreVal(string pre) {
    stack<int> st;
    int n = pre.length();
    
    for(int i=n-1; i>=0; i--) {
        char c = pre[i];
        
        if(isdigit(c)) {
            int num = 0;
            
            while(i >= 0 && isdigit(pre[i])) {
                num = num * 10 + pre[i] - '0';
                i--;
            }
            
            st.push(num);
        } 
        
        else {
            
            int first = st.top();
            st.pop();
            int second = st.top();
            st.pop();
            
            // cout<<first<<" "<<second<<endl;
            
            if(c == '^') {
                st.push(pow(first, second));
            }
            
            else if(c == '*') {
                st.push(first * second);
            }
            
            else if(c == '/') {
                st.push(first / second);
            }
            
            else if(c == '+') {
                st.push(first + second);
            }
            
            else if(c == '-') {
                st.push(first - second);
            }
        }
    }
    
    return st.top();
}

int main() {
	
	string str = "254+3*(55^1-3)";
	
	
	string postfix = convertToPostFix(str);
	
	cout<<postfix<<endl;
	cout<<getVal(postfix)<<endl;
	
	string prefix = convertToPrefix(str);
	cout<<prefix<<endl;
	cout<<getPreVal(prefix)<<endl;

}

```

## Complexity Analysis:

### Time Complexity: O(N)

### Space Complexity: (N)
