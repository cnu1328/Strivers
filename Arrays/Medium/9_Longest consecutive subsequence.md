# Longest consecutive subsequence

[Problem Link](https://www.geeksforgeeks.org/problems/longest-consecutive-subsequence2449/1)

## Approach - 1 - Brute Force

1. We will traverse in the array, for every element we check for next number is exit or not by linear search. If next number exists, then I will search for next number.. I will search till no element next element exist.
2. we always count how many numbers existed
3. we will maximize the count and return the answer

```Java


class Solution{
  public:


    bool linS(int arr[], int x, int N) {
        for(int i=0; i<N ;i++) {
            if(arr[i] == x) {
                return true;
            }
        }

        return false;
    }
    // arr[] : the input array
    // N : size of the array arr[]

    //Function to return length of longest subsequence of consecutive integers.
    int findLongestConseqSubseq(int arr[], int N)
    {
      //Brute Force Approach

      int largest = 1;

      for(int i=0; i<N; i++) {
          int x = arr[i];
          int cnt = 1;
          while(linS(arr,x+1,N) == true) {
              x = x+1;
              cnt++;
          }

          largest = max(largest,cnt);
      }

      return largest;
    }
};


```

## Complexity Analysis:

### Time Complexity: O(N^2)

### Space Complexity: O(1)

## Approach - 2 - Better

1. Sort the given array
2. Find the length of largest consecutive elements
3. return the answer

```Java

class Solution{
  public:
    int findLongestConseqSubseq(int arr[], int N)
    {


      //Better Approach

      sort(arr,arr+N); //O(nlogn)

      int largest = 1,curr_count = 0, prev_smaller = INT_MIN;

      for(int i=0; i<N; i++) {

          if(arr[i]-1 == prev_smaller) {
              curr_count++;
              prev_smaller = arr[i];
          }

          else if(arr[i] != prev_smaller) {
              curr_count = 1;
              prev_smaller = arr[i];
          }

          largest = max(largest,curr_count);
      }

      return largest;
    }
};

```

## Complexity Analysis:

### Time Complexity: O(N \* Log n)

### Space Complexity: O(1)

## Approach - 3 - Optimal

1. Use a set, and insert all the array elements to it
2. Then, Traverse the Set, Check first the element is first element of sequence, if it is then check for next consecutive elements.
3. Increment the count and find maximum count
4. return the answer

```Java

class Solution{
  public:
    // arr[] : the input array
    // N : size of the array arr[]

    //Function to return length of longest subsequence of consecutive integers.
    int findLongestConseqSubseq(int arr[], int N)
    {
        int longestConseq = 1;

        if(N == 0) {
            return 0;
        }

        unordered_set<int> unique;

        for(int i=0; i<N; i++) {
            unique.insert(arr[i]);
        }

        for(auto item : unique) {
            if(unique.find(item-1) == unique.end() ) {
                int curr_count = 1;
                int curr_ele = item;
                while(unique.find(curr_ele +1) != unique.end()) {
                    curr_count++;
                    curr_ele++;
                }

                longestConseq = max(longestConseq,curr_count);
            }

        }

        return longestConseq;
    }
};

```

## Complexity Analysis:

### Time Complexity: O(N \* Log n)

### Space Complexity: O(N)
