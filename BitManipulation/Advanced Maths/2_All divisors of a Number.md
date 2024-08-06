# All divisors of a Number

[Problem Link](https://www.geeksforgeeks.org/problems/all-divisors-of-a-number/1)

## Approach - 1

1. Traverse the loop till its square root of N
2. if `i` divides a number, then (n / i) also divides the number.
3. Let's take 4 divides 20, then 20/4 = 5 also divides the number
4. return all the divisors

```c++

class Solution {
  public:
    void print_divisors(int n) {

        vector<int> ans;
        for(int i=1; i*i <= n; i++) {
            if(n % i ==0 ) {
                ans.push_back(i);

                if(n/i != i)
                    ans.push_back(n/i);
            }
        }

        sort(ans.begin(), ans.end());

        for(int ele : ans) {
            cout<<ele<<" ";
        }
    }
};

```

## Complexity Analysis:

### Time Complexity: O(sqrt(N))

### Space Complexity: (divisors)
