# Count number of substrings

[Problem Link](https://www.geeksforgeeks.org/problems/count-number-of-substrings4528/1)

## Approach - 1

1. Generate all the substring, and count number of distinct characters in that substring
2. If the count of distinct characters is equal to K, then increment answer by 1

## Complexity Analysis:

### Time Complexity: O(N \* N)

### Space Complexity: (1)

## Approach - 2

1. Finding the number of substrings with exactly K distinct elements seems a tough task with sliding window.
2. But, we can easily find the number of substrings with at most K distinct characters using sliding window.
3. So, the number of substrings with exactly K distinct characters = number of substrings with at most K distinct characters - number of substrings with at most K-1 distinct characters.
4. Calculate the number of substrings
   - Declare frequency array and dist_char
   - Traverse the given string (i)
     - If the frequency of character is equal to `1` then increment dist_char
     - while loop, if the dist_char > K (j)
       - reduce the frequency from left(i) and if the frequency becomes zero, then decrement dist_char
     - add the length of the substring to ans
   - return the answer

```Java

class Solution
{
  public:
    long long int atMostK (string s, int k)
    {
    	if (k < 0) return 0;

    	int i = 0, j = 0, dist_char = 0;
    	long long int res = 0;
    	int m[26] = {0};

    	while (j < s.length ())
    	{
    		m[s[j] - 'a']++;
    		if (m[s[j] - 'a'] == 1) dist_char++;

    		while (dist_char > k)
    		{
    			m[s[i] - 'a']--;
    			if (m[s[i] - 'a'] == 0) dist_char--;

    			i++;
    		}

    		res += (j - i + 1);
    		j++;
    	}
    	return res;
    }

    long long int substrCount (string s, int k) {
    	return atMostK (s, k) - atMostK (s, k - 1);
    }
};

```

## Complexity Analysis:

### Time Complexity: O(N)

### Space Complexity: (1)
