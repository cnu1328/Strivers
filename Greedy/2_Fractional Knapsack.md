# Fractional Knapsack

[Problem Link](https://www.geeksforgeeks.org/problems/fractional-knapsack-1587115620/1)

## Approach - 1

1. Sort the values based on the the (value[i]/weight[i])
2. Traverse from the first
3. If we can take all the weight, then add value[i] to our answer, and decrement weight by weight[i
4. If we can't then add its fractional weight (value[i]/weight[i]) gives us the fraction, then multiply it with remaining weigh
5. return the answer

```c++


class Solution
{
    public:

    static bool comp(Item a, Item b) {
        return (double)a.value/a.weight > (double)b.value/b.weight;
    }

    double fractionalKnapsack(int W, Item arr[], int n)
    {
        sort(arr, arr + n, comp);

        for(int i=0; i<n; i++) {
            cout<<arr[i].weight<<" "<<arr[i].value<<endl;
        }

        double ans = 0;

        for(int i=0; i<n; i++) {
            if(arr[i].weight <= W) {
                ans += arr[i].value;
                W -= arr[i].weight;
            } else {
                ans += ((double)arr[i].value/arr[i].weight)*(double)W;
                break;
            }
        }

        return ans;
    }

};

```

## Complexity Analysis:

### Time Complexity: O(Log N + N)

### Space Complexity: (1)
