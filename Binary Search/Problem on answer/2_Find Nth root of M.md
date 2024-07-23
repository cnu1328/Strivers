# Find Nth root of M

[Problem Link](https://www.geeksforgeeks.org/problems/find-nth-root-of-m5843/1)

## Approach - 1 - Linear Search

1. We can guarantee that our answer will lie between the range from 1 to m i.e. the given number.
2. So, we will perform a linear search on this range and we will find the number x, such that func(x, n) = m. If no such number exists, we will return -1.

**Note: func(x, n) returns the value of x raised to the power n i.e. xn.**

```Java

// Power exponential method:
public static long func(int b, int exp) {
    long  ans = 1;
    long base = b;
    while (exp > 0) {
        if (exp % 2 == 1) {
            exp--;
            ans = ans * base;
        } else {
            exp /= 2;
            base = base * base;
        }
    }
    return ans;
}

public static int NthRoot(int n, int m) {
    //Use linear search on the answer space:
    for (int i = 1; i <= m; i++) {
        long val = func(i, n);
        if (val == (long)m) return i;
        else if (val > (long)m) break;
    }
    return -1;
}

```

## Complexity Analysis:

### Time Complexity: O(M)

### Space Complexity: O(1)

## Approach - 2 - Using Binary Search

1. Perform binary search on search space and return the appropriate answer

```Java

class Solution
{
    public int NthRoot(int n, int m)
    {
        long low = 1L, high = (long)m;
        long ans = -1L;

        while(low <= high) {
            long mid = (low + high)/2;

            double val = Math.pow(mid, (long)n);

            if(val == (double)m) {
                return (int)mid;
            }

            if(val < (double)m) {
                low = mid + 1;
            } else {
                high = mid - 1;
            }
        }

        return -1;
    }
}

```

## Complexity Analysis:

### Time Complexity: O(Log M)

### Space Complexity: O(1)
