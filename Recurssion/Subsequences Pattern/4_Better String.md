# Better String

[Problem Link](https://www.geeksforgeeks.org/problems/better-string/1)

## Approach 

1. The main idea is to count the number of distinct subsequences of two strings, if any one of strings count is greater than return that string. if count is equal then return str1
2. Here we need to optimize the count of distinct subsequences.
3. we can do with the help of memoization, first take a map<char, int>
4. As you, if you include a character, then its number of subsequences is multiplied by 2
    - for two characters we have "ab" - number of subsequences 4
    - if I add c to the above string => "abc", then number of subsequences are multiplied by 2 right. so its number of subsequences are 8
5. So, we traverse the string, for everytime, we find number of subsequences as a newCount.
6. We check if current character exit in map, if so decrement the newCount by mp[current character]

7. Then assign the current character with count value, initially the count = 1
8. and assign count with newCount
9. return the count

```Java

class Solution {
    
    private static int distSubCount(String str) {
        
        Map<Character, Integer> last = new HashMap<>();
        int count = 1;
        
        for(int i=0; i<str.length(); i++) {
            
            char s = str.charAt(i);
            
            int newCount = 2 * count;
            
            if(last.containsKey(s)) {
                newCount -= last.get(s);
            }
            
            last.put(s, count);
            count = newCount;
        }
        
        return count;
    }
    
    public static String betterString(String str1, String str2) {
        // Code here
        int better1 = distSubCount(str1);
        int better2 = distSubCount(str2);
        
        return better1 >= better2 ? str1 : str2;
    }
}

```

## Complexity Analysis:

### Time Complexity: O(N) 

### Space Complexity: O(N)