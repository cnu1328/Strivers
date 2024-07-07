# Union of Two Sorted Arrays

[Problem Link](https://www.geeksforgeeks.org/problems/union-of-two-sorted-arrays-1587115621/1)

## Approach - 1 - Brute Force Approach

1. Use a Set, and insert all the array 1 and array 2 elements to it
2. Declare an another array, and push all the elements to it from set
3. return the resultant array

```Java

class Solution{
    public:
    vector<int> findUnion(int arr1[], int arr2[], int n, int m)
    {
        //Brute Force Approach
        set<int> st;
        for(int i=0;i<n;i++){
            st.insert(arr1[i]);
        }
        for(int j=0;j<m;j++){
            st.insert(arr2[j]);
        }
        vector<int> v;
        for(auto it : st){
            v.push_back(it);
        }

        return v;
    }
};

```

## Complexity Analysis:

### Time Complexity: O(N \* Log (N))

### Space Complexity: O(number of unique elements)

## Approach - 2 - Two Pointers

1. As we know the array is sorted, we can simply check which elements come first and which element take only once(if there are duplicates)
2. Check if which element comes first, and if the element will not exist on the last index of resultant array, then push the element to resultant array
3. If the element is existed then do nothing
4. We are given two different size of arrays, so we check till the minimum size of array
5. The remainig element directly added, by checking the last index element
6. return the final answer

```Java

class Solution{
    public:
    vector<int> findUnion(int arr1[], int arr2[], int n, int m)
    {
        int i=0,j=0;

        vector<int> v;
        while(i<n && j<m){
            if(arr1[i]<=arr2[j]){
                if(v.size() == 0 || v.back() != arr1[i]){
                    v.push_back(arr1[i]);
                }
                i++;
            }
            else{
                if(v.size() == 0 || v.back() != arr2[j]){
                    v.push_back(arr2[j]);
                }
                j++;

            }
        }

        while(i<n){
            if(v.size() == 0 || v.back() != arr1[i]){
                    v.push_back(arr1[i]);
            }
            i++;
        }

        while(j<m){
            if(v.size() == 0 || v.back() != arr2[j]){
                    v.push_back(arr2[j]);
            }
            j++;
        }

        return v;
    }
};

```

## Complexity Analysis:

### Time Complexity: O(N + M)

### Space Complexity: O(number of unique elements)
