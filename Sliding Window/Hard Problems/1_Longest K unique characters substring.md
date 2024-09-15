# Longest K unique characters substring

[Problem link](https://www.geeksforgeeks.org/problems/longest-k-unique-characters-substring0853/1)

## Approach - 1

1. Declare map, and find frequency of each character
2. The map size tells that, the number of characters(unique)
3. If map size greater than K, then decremenet the window(left ++)
4. If map size is equal to K, then find the maximum window

```c++

class Solution{
  public:
    int longestKSubstr(string s, int k) {
        unordered_map<char, int> mp;
        int left = 0, right = 0;
        int n = s.length();
        int ans = 0;

        while(right < n) {
            mp[s[right]] ++;

            while(mp.size() > k) {
                mp[s[left]] --;

                if(mp[s[left]] == 0) {
                    mp.erase(s[left]);
                }

                left ++;
            }

            if(mp.size() == k) {
                ans = max(ans, right - left + 1);
            }

            right ++;
        }

        return ans == 0 ? -1 : ans;
    }
};

```

## Complexitiy Analysis:

### Time Complexity : O(N)

### Space Compleixty : O(1)
