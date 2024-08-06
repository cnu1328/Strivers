# Prime Factors

[Problem Link](https://takeuforward.org/strivers-a2z-dsa-course/strivers-a2z-dsa-course-sheet-2)

## Approach - 1

1. Traverse a loop from 2 to N as num
2. Check if `N % num == 0`, then the num is one of the prime factor
3. Push num to answer vector and, check try to remove its powers
4. Loop until the num divides the N, every time divide the N by num

```c++

class Solution{
	public:
	vector<int>AllPrimeFactors(int N) {

	    vector<int> ans;

	    for(int num = 2; num <= N; num++) {

	        if(N % num == 0) {

	            ans.push_back(num);

	            while(N % num == 0) {
	                N  = N / num;
	            }
	        }
	    }

	    return ans;
	}
};

```

## Complexity Analysis:

### Time Complexity: O(N \* log N)

### Space Complexity: (1)
