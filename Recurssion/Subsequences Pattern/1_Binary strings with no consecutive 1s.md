# Binary strings with no consecutive 1s.

[Problem Link](https://www.naukri.com/code360/problems/binary-strings-with-no-consecutive-1s_893001)


## Approach 

1. The question asking as to return the binary strings with no consecutive 1s.
2. suppose, if the last character of the string is '0' in this case we have two options to take either 0 or 1 as next character
3. or if the last character of the string is '1' in this case we have only one option that is, i can take next character as '0'
4. retun the vector of strings

```Java


void generate(int n, string curr, vector<string> &binary) {
    if(n == 0) {
        binary.push_back(curr);
        return;
    }

    
    if(curr.length() == 0 || curr[curr.length() -1] == '0') {
        generate(n-1, curr + '0', binary);
        generate(n-1, curr + '1', binary);
    }

    else {
        generate(n-1, curr + '0', binary);
    }
    
}

vector<string> generateString(int N) {
    vector<string> binary;
    
    generate(N, "", binary);

    return binary;
}

```


## Complexity Analysis:

### Time Complexity: O(2^N) 

### Space Complexity: O(N)