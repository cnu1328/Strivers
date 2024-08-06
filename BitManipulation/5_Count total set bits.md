# Count total set bits

[Problem Link](https://www.geeksforgeeks.org/problems/count-total-set-bits-1587115620/1)

## Approach - 1

1. Every time divide the given number by 2
2. And perform and operation to it, if results is 1, then increment the count

```c++

int countSetBits(int N)
{
    int count = 0;
    for(int i = 1; i<=N; i++) {

        int cnt = 0;
        int n = i;

        while(n > 0) {
            n = n & (n-1);
            cnt++;
            // if(n & 1) {
            //     cnt++;
            // }

            // n >>= 1;
        }

        count += cnt;
    }

    return count;

}

```

## Complexity Analysis:

### Time Complexity: O(N \* Log N)

### Space Complexity: (1)
