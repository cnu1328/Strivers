# Set the rightmost unset bit

[Problem Link](https://www.geeksforgeeks.org/problems/set-the-rightmost-unset-bit4436/1)

## Approach - 1

1. First find the unset bit(the count from right most)
2. Then make the unsert bit to set
3. return the answer

```c++

class Solution {
  public:
    int setBit(int n) {

        int count = 0;
        int num = n;

        while(num > 0) {
            if(num&1) {
                count++;
            }  else {
                break;
            }

            num = num >> 1;
        }


        return (n | (1 << count));
    }
};

```

## Complexity Analysis:

### Time Complexity: O(Log N)

### Space Complexity: (1)
