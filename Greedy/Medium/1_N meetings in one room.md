# N meetings in one room

[Problem Link](https://www.geeksforgeeks.org/problems/n-meetings-in-one-room-1587115620/1)

## Approach - 1

1. sort the array based on the end time
2. Then check if the prev endtime is less than current end time, then increment the answer and change the index to current index
3. return the count

```c++

class Solution
{
    public:

    static bool comp(pair<int, int> a, pair<int, int> b) {
        return a.second < b.second;
    }

    int maxMeetings(int start[], int end[], int n)
    {
        vector<pair<int, int>> pr;

        for(int i=0; i<n; i++) {
            pr.push_back({start[i], end[i]});
        }

        sort(pr.begin(), pr.end(), comp);

        int ans = 1;
        int index = 0;

        for(int i=1; i<n ;i++) {

            if(pr[index].second < pr[i].first) {
                ans++;
                index = i;
            }

        }

        return ans;
    }
};


```

## Complexity Analysis:

### Time Complexity: O(Log N + N)

### Space Complexity: (1)
