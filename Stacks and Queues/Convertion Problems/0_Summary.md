# Infix to PostFix

1. First, traverse the given string from first
2. Get, the number and seperate it with '#' and push to the answer
3. If c == `(`, push to the stack
4. If c == `)`, then pop from stack and push to answer, till st.top() == `(`
5. Perform Infix to postfix with controlled(i.e, precedence[s[i]] <= precedence[st.top()]), if so push to the answer and perform st.pop(), If condition failed st.push(s[i])
6. If stack has any operators, then push to the answer
7. return the resultant string

# Infix to Prefix

1. First, reverse the given string and traverse from first
2. Get, the number and seperate it with '#' and push to the answer
3. If c == `)`, push to the stack
4. If c == `(`, then pop from stack and push to answer, till st.top() == `)`
5. Perform Infix to prefix with controlled(i.e, precedence[s[i]] < precedence[st.top()]), if so push to the answer and perform st.pop(), If condition failed st.push(s[i])
6. If stack has any operators, then push to the answer
7. reverse the string
8. return the resultant string

## PostFix to Infix

1. Traverse given string from first
2. When you find a operand('a') then push to the stack
3. When a current character is operator('+' - etc.,) then take two operands from the stack, first one as `second` and second as `first`
4. Then push to the stack => `'(' + first + c + second + ')'`

## Prefix to Infix

1. Traverse given string from last
2. When you find a operand('a') then push to the stack
3. When a current character is operator('+' - etc.,) then take two operands from the stack, first one as `first` and second as `second`
4. Then push to the stack => `'(' + first + c + second + ')'`

## prefix to postfix

1. Traverse given string from last
2. When you find a operand('a') then push to the stack
3. When a current character is operator('+' - etc.,) then take two operands from the stack, first one as `first` and second as `second`
4. Then push to the stack => `first +  second + c`

## postfix to prefix

1. Traverse given string from first
2. When you find a operand('a') then push to the stack
3. When a current character is operator('+' - etc.,) then take two operands from the stack, first one as `second` and second as `first`
4. Then push to the stack => `c + first +  second`
