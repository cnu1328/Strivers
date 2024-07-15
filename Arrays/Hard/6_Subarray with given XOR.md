# Subarray with given XOR

[Problem Link](https://www.interviewbit.com/problems/subarray-with-given-xor/)

## Approach - 1

1. Generate all sub-arrays and check if xor of subarray equals to K
2. If equals then increment the answer and return it

## Complexity Analysis:

### Time Complexity: O(N^2)

### Space Complexity: O(1)

## Approach - 2

1. Use HashMap and prefix Xor concept to solve this problem
2. calculate the prefix xor for the array, while calculating, check if the prefixXor ^ K is present in the mp. If present increment the answer by its count
3. else increment the prefixXor map count
4. return the answer

```Java




import java.util.*;

public class tUf {

    public static int subarraysWithXorK(int []a, int k) {
        int n = a.length; //size of the given array.
        int xr = 0;
        Map<Integer, Integer> mpp = new HashMap<>(); //declaring the map.
        mpp.put(xr, 1); //setting the value of 0.
        int cnt = 0;

        for (int i = 0; i < n; i++) {
            // prefix XOR till index i:
            xr = xr ^ a[i];

            //By formula: x = xr^k:
            int x = xr ^ k;

            // add the occurrence of xr^k
            // to the count:
            if (mpp.containsKey(x)) {
                cnt += mpp.get(x);
            }

            // Insert the prefix xor till index i
            // into the map:
            if (mpp.containsKey(xr)) {
                mpp.put(xr, mpp.get(xr) + 1);
            } else {
                mpp.put(xr, 1);
            }
        }
        return cnt;
    }

    public static void main(String[] args) {
        int[] a = {4, 2, 2, 6, 4};
        int k = 6;
        int ans = subarraysWithXorK(a, k);
        System.out.println("The number of subarrays with XOR k is: " + ans);
    }
}


```

## Complexity Analysis:

### Time Complexity: O(N)

### Space Complexity: O(N)
