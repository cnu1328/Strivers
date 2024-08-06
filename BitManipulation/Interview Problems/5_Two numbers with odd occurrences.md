# Two numbers with odd occurrences

[Problem Link](https://www.geeksforgeeks.org/problems/two-numbers-with-odd-occurrences5846/1)

## Approach - 1

1. First find the xor of all elements
2. Now you only left with two elements that are odd in xor form like (5 ^ 1)
3. Find the set bit, where two numbers are differing
4. Based on this, seperate the array elements to two groups
5. And xor them, to get the two odd numbers

```c++

class Solution{
    public:
    vector<long long int> twoOddNum(long long int arr[], long long int n)
    {
        long long int xr = 0;

        for(int i=0; i<n; i++) {
            xr ^= arr[i];
        }

        int count = 0;

        while (xr > 0) {
            if(xr & 1) {
                break;
            }

            count++;

            xr >>= 1;
        }

        long long int xr1 = 0;
        long long int xr2 = 0;


        for(int i=0; i<n; i++) {

            if(arr[i] & (1 << count)) {
                xr1 ^= arr[i];
            } else {
                xr2 ^= arr[i];
            }
        }

        if(xr1 > xr2) {
            return {xr1, xr2};
        }

        return {xr2, xr1};
    }
};


```

## Complexity Analysis:

### Time Complexity: O(N)

### Space Complexity: (1)
