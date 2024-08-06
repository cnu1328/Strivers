# Bit Manipulation

[Problem Link](https://www.geeksforgeeks.org/problems/bit-manipulation-1666686020/1)

## Approach - 1

1. To get ith bit => (num >> i) & 1
   - 10100 => right shift three times
   - resultant 101
   - do and with 1
   - 101 & 1 => 1
   - the ith bit is set
2. To set the ith bit =>

   - (1 << i) to create a mask
   - num | (mask)
   - will set the bit

3. Clear ith bit of a number

   - First create a mask (1 << i)
   - 1 << 2 => 100
   - then negate the mask => ~(mask) => (011) say mask1
   - Now, Do and with given num
   - num & (mask1)

```java

class Solution {
  public:
    void bitManipulation(int num, int i) {
        // your code here
        int mask = 1<<(i-1);
        int mask1 = ~(1 << (i-1));


        cout<<(num>>(i-1) & 1)<<" "<<(num | mask)<<" "<<(num & mask1);
    }
};

```

## Complexity Analysis:

### Time Complexity: O(1)

### Space Complexity: (1)
