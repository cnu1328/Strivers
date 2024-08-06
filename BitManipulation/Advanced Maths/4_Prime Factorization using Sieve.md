# Prime Factorization using Sieve

[Problem Link](https://www.geeksforgeeks.org/problems/prime-factorization-using-sieve/1)

## Approach - 1

1. Pre-compute the sieve
2. For every prime number, check is it divisble by prime number
3. If it is divisible then add the I to answer list
4. Loop until it is not divisible

```c++

class Solution {
  public:
    void sieve() {}

    vector<int> findPrimeFactors(int N) {

        vector<bool> sieve(N + 1, true);

        sieve[0] = sieve[1] = false;

        vector<int> ans;

        for(int i=2; i * i <= N; i++) {

            if(sieve[i]) {
                for(int j = i * i; j <= N; j += i) {
                    sieve[j] = false;
                }
            }
        }

        for(int i=2; i<=N; i++) {

            if(sieve[i] && N % i == 0) {

                while(N % i == 0) {
                    ans.push_back(i);
                    N = N / i;
                }
            }
        }

        return ans;
    }
};

```

## Complexity Analysis:

### Time Complexity: O(N + Log(Log(n)))

### Space Complexity: (N)
