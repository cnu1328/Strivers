# Missing And Repeating

[Problem Link](https://www.geeksforgeeks.org/problems/find-missing-and-repeating2512/1)

## Approach - 1

1. Use linear search to find the count of each number, if count equal to zero(missing number) and count equal to two(repeating number)

## Complexity Analysis:

### Time Complexity: O(N ^ 2)

### Space Complexity: O(1)

## Approach - 2 - Use Hash Array

1. Declare a hash with given size
2. Update its frequency when we get an element in the array
3. Check if the given element size if two or zero, perform accordingly
4. return the answer

## Complexity Analysis:

### Time Complexity: O(N)

### Space Complexity: O(N)

## Approach - 3 - Using Math

1. We know the sum of first natural numbers is `n * (n + 1) / 2` as Sn
2. we know the sum of first square natural numbers is `n * (n + 1) * (2 * n + 1) / 2` as Ssn
3. Let say, X is repeating number and Y is missing number
4. Find the sum of numbers in the given array - `arrSum`
5. Find the square of numbers from the given array - `arrSsum`
6. We have a formula that, `X - Y = arrSum - Sn`
7. and `X^2 - Y^2 = arrSsum - Ssn`
8. From (7.) we can write as, `X + Y = (arrSum - Sn) / X-Y`
9. From (6.) and (7.) we can find the missing and repeating number

```Java

class Solve {
    int[] findTwoElement(int arr[], int m) {
        // code here
        long n = (long)m;
        long Sn = (n * (n + 1))/2;
        long Ssn = (n * (n + 1) * (2*n + 1))/6;

        long arrSum = 0;
        long arrSsum = 0;

        for(int i=0; i<n; i++) {
            arrSum += arr[i];
            arrSsum += (long)arr[i]*(long)arr[i];
        }

        long xminusy = arrSum - Sn;


        long xplusy = (arrSsum - Ssn)/xminusy;

        int repeat = (int)((xplusy + xminusy)/2);
        int missing = (int)(repeat - xminusy);

        int ans[] = {repeat, missing};

        return ans;
    }
}

```

## Complexity Analysis:

### Time Complexity: O(N)

### Space Complexity: O(1)

## Approach - 4 - Using Xor

```Java

class Solution {
  public:
    vector<int> findTwoElement(vector<int>& arr) {
        
        int xr = 0;
        int n = arr.size();
        
        for(int i=0; i<n; i++) {
            xr = xr ^ arr[i] ^ (i + 1);
        }
        
        int count = 0;
        
        while(xr > 0) {
            if(xr & 1) {
                break;
            }
            
            count ++;
            xr >>= 1;
        }
        
        int ele1 = 0, ele2 = 0;
        
        for(int i=0; i<n; i++) {
            if((arr[i]>>count) & 1) {
                ele1 ^= arr[i];
            }
            
            else {
                ele2 ^= arr[i];
            }
            
            if(((i + 1) >> count) & 1) {
                ele1 ^= (i + 1);
            }
            
            else {
                ele2 ^= (i + 1);
            }
        }
        
        int count1 = 0, count2 = 0;
        
        for(int ele : arr) {
            if(ele1 == ele) count1 ++;
            if(ele2 == ele) count2 ++;
        }
        
        if(count1 == 2) {
            return {ele1, ele2};
        }
        
        return {ele2, ele1};
    }
};

```

## Complexity Analysis:

### Time Complexity: O(N)

### Space Complexity: O(1)
