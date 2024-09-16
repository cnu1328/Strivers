# Job Sequencing Problem

[Problem Link](https://www.geeksforgeeks.org/problems/job-sequencing-problem-1587115620/1)

## Approach - 1

1. First sort the given array, based on the profit in decreasing order
2. Find the maximum deadline and create an array for it and declare all the values with -1
3. Traverse the job array,
   - Traverse the array with Job deadline till 1
   - check is the slot is -1, if so increament the job count and and increment the profit and break from there by changing the slot value
4. return {jobs, profit}

```c++

class Solution
{
    public:

    static bool comp(Job a, Job b) {
        return a.profit > b.profit;
    }

    //Function to find the maximum profit and the number of jobs done.
    vector<int> JobScheduling(Job arr[], int n)
    {
        sort(arr, arr + n, comp);

        int maxi = arr[0].dead;

        for(int i=1; i<n; i++) {
            maxi = max(maxi, arr[i].dead);
        }

        int slot[maxi + 1];

        for(int i=0; i<=maxi; i++) {
            slot[i] = -1;
        }

        int jobs = 0, profit = 0;

        for(int i=0; i<n; i++) {
            for(int j=arr[i].dead; j>0; j--) {

                if(slot[j] == -1) {
                    jobs++;
                    slot[j] = 1;
                    profit += arr[i].profit;

                    break;
                }
            }
        }

        return {jobs, profit};

    }
};

```

## Complexity Analysis:

### Time Complexity: O(N ^ 2)

### Space Complexity: (1)

## Approach - 2

1. First sort the given jobs based on the deadline in ascending order
2. Then declare a min-heap and curr_deadline is 1
3. If arr[i].dead >= curr_deadline, means we can take this and push the profit to the mheap and increment the curr_deadline
4. If not, then the present arr[i].profit > mheap.top(), then pop the top profit form mheap and push arr[i].profit to the mheap
5. After array traversal, traverse the mheap and find the jobs and profit
6. return {jobs, profit}

```c++

class Solution 
{
    public:
    
    static bool comp(Job a, Job b) {
        return a.dead < b.dead;
    } 
    
    
    vector<int> JobScheduling(Job arr[], int n) 
    { 
        sort(arr, arr + n, comp);
        
        priority_queue<int, vector<int>, greater<>> mheap;
        
        int curr = 1;
        
        for(int i=0; i<n; i++) {
            if(arr[i].dead >= curr) {
                mheap.push(arr[i].profit);
                curr ++;
            }
            
            else if(arr[i].profit > mheap.top()) {
                mheap.pop();
                mheap.push(arr[i].profit);
            }
        }
        
        vector<int> ans;
        
        int jobs = 0, profit = 0;
        
        while(!mheap.empty()) {
            jobs ++;
            profit += mheap.top();
            mheap.pop();
        }
        
        return {jobs, profit};
    } 
};

```

## Complexity Analysis:

### Time Complexity: O(N * Log N)

### Space Complexity: (1)
