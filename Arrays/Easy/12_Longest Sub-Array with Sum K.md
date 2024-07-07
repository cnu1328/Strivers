# Longest Sub-Array with Sum K

[Problem Link](https://www.geeksforgeeks.org/problems/longest-sub-array-with-sum-k0809/1)

## Approach - 1

1. Try out all sub-arrays, if you find sub-array sum is equals to K, then find max Length of it
2. return max Length of sub-array, whose sum is equals to K

```Java

class Solution{
    public:
    int lenOfLongSubarr(int A[],  int N, int K)
    {
        int len = 0;

        for(int i=0;i<N;i++){
            long long sum = 0;
            for(int j=i;j<N;j++){
                sum += A[j];
                if(sum==K)
                    len = max(len,j-i+1);

            }
        }
        return len;
    }

};

```

## Complexity Analysis:

### Time Complexity: O(N^2)

### Space Complexity: O(1)

## Approach - 2

1. The main idea of this approach is that, let say sum of sub-array at index `i` is X.
2. We check if there exist any subarray in the sub-array ending at index `i` which has sum is equal to K.
3. We will find by checking if X-K is exist in the map. If exist, then there exist a sub-array with sum K
4. In this approach, we use HashMap, the prefixSum and index.
5. First we will check, if prefixSum is equal to the K, if so, then length is `i+1`
6. Then after, we will check if `prefixSum - k` exist in the map, if so the length is `i - map[preixSum - k]`
7. If not exist, then insert prefixSum to the map
8. Return the max subarray length, whose sum is K

```Java

class Solution{
    public:
    int lenOfLongSubarr(int A[],  int N, int K)
    {
        map<long long,int> prefixSum;

        long sum = 0;
        int maxlen=0;
        for(int i=0;i<N;i++){
            sum += A[i];

            if(sum==K)
                maxlen = max(maxlen,i+1);
            long long rem = sum-K;
            if(prefixSum.find(rem) != prefixSum.end()){
                int len=i-prefixSum[rem];
                maxlen = max(maxlen,len);
            }
            if(prefixSum.find(sum)==prefixSum.end())
                prefixSum[sum]=i;
        }

        return maxlen;
    }
};

```

## Complexity Analysis:

### Time Complexity: O(N)

### Space Complexity: O(N)

## Approach - 3

1. We are using two pointers i.e. left and right.
2. The left pointer denotes the starting index of the subarray and the right pointer denotes the ending index.
3. Now as we want the longest subarray, we will move the right pointer in a forward direction every time adding the element i.e. a[right] to the sum.
4. But when the sum of the subarray crosses k, we will move the left pointer in the forward direction as well to shrink the size of the subarray as well as to decrease the sum.
5. Thus, we will consider the length of the subarray whenever the sum becomes equal to k.

The below dry run will clarify the intuition.

![Probelm ](https://static.takeuforward.org/wp/uploads/2023/04/Screenshot-2023-04-13-012512.png)

```Java

public static int getLongestSubarray(int []a, long k) {
    int n = a.length; // size of the array.

    int left = 0, right = 0; // 2 pointers
    long sum = a[0];
    int maxLen = 0;
    while (right < n) {
        // if sum > k, reduce the subarray from left
        // until sum becomes less or equal to k:
        while (left <= right && sum > k) {
            sum -= a[left];
            left++;
        }

        // if sum = k, update the maxLen i.e. answer:
        if (sum == k) {
            maxLen = Math.max(maxLen, right - left + 1);
        }

        // Move forward thw right pointer:
        right++;
        if (right < n) sum += a[right];
    }

    return maxLen;
}

```

## Complexity Analysis:

### Time Complexity: O(2\*N)

### Space Complexity: O(1)
