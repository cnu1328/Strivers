# Subset Sum

[Problem Link](https://www.naukri.com/code360/problems/subset-sum_630213)

## Approach - Recurssion

1. Implement take or not take element, and if any where you found a subsequence then return true, then stop all the recurssions further simply return true

```Java



bool sos(int index, int k, vector<int> &a) {
    

    if(k < 0) return false;

    if(index < 0) {
        if(k == 0) return true;
        return false;
    }

    if(sos(index - 1, k - a[index], a)) return true;

    if(sos(index - 1, k, a)) return true;

    return false;
}


bool isSubsetPresent(int n, int k, vector<int> &a)
{
    return sos(n-1, k, a);
}

```

## Complexity Analysis:

### Time Complexity: O(2^N) 

### Space Complexity: O(N) 