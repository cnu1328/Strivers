# Array Leaders

[Problem Link](https://www.geeksforgeeks.org/problems/leaders-in-an-array-1587115620/1)

## Approach - 1 - Brute Force

1. For a element, check if all the right side elements are less than current element.
2. In this case, the current element is Leader, push this current element to answer

```Java



class Solution{
    //Function to find the leaders in the array.
    public:
    vector<int> leaders(int a[], int n){
        //Brute Force

        vector<int> v;

        for(int i=0; i<n; i++) {
            bool leader = true;

            for(int j = i+1; j<n; j++) {
                if(a[i]<a[j]){
                    leader = false;
                    break;
                }
            }

            if(leader == true) {
                v.push_back(a[i]);
            }
        }


        return v;

    }
};

```

## Complexity Analysis:

### Time Complexity: O(N^2)

### Space Complexity: O(N)

## Approach - 2 - Optimal

1. Traverse the array form the last index, the element at `n-1` index is always a leader.
2. Check for every index if the the current element is greater than or equal to the previous leader, then add the current element to out answer list.
3. After traversal, reverse the answer array and return the answer

```Java



class Solution{
    //Function to find the leaders in the array.
    public:
    vector<int> leaders(int a[], int n){
        vector<int> leader;

        leader.push_back(a[n-1]);

        for(int i=n-2; i>=0; i--) {
            if(a[i] >= leader.back()) {
                leader.push_back(a[i]);
            }
        }

        reverse(leader.begin(), leader.end());

        return leader;

    }
};

```

## Complexity Analysis:

### Time Complexity: O(N)

### Space Complexity: O(N)
