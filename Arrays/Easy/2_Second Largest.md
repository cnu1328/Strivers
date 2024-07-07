# Second Largest

[Problem Link](https://www.geeksforgeeks.org/problems/second-largest3735/1)

## Approach - 1 - Two Pass

1. First find the first largest element seperately
2. Then traverse the loop again and find the second largest element, like the current element should be greater than prev second max and less than largest element
3. return the answer

```Java

class Solution{
public:

	int print2largest(int arr[], int n) {
	   if(n==0 || n==1){
	       return -1;
	   }

	   int large,s_large;

	   large = s_large = INT_MIN;

	   for(int i=0;i<n;i++){
	       large = max(arr[i],large);
	   }

	   for(int i=0;i<n;i++){
	       if(arr[i]>s_large && arr[i]!=large)
	            s_large = arr[i];
	   }

	   if(s_large == INT_MIN)
	        return -1;

	   return s_large;


	}
};

```

## Complexity Analysis:

### Time Complexity: O(N)

### Space Complexity: O(1)

## Approach - 2 - One Pass

1. On the fly we calculate the max and second max elements and returns second max element
2. If you find an element greater than max element, then assign max to second max and element to max
3. If you find an element less than max and greater than second max, then assign the element to second max
4. return the answer

```Java

class Solution{
public:

	int print2largest(int arr[], int n) {
	   if(n==0 || n==1){
	       return -1;
	   }

	   int max,s_max;

	   max = s_max = INT_MIN;

	   for(int i=0;i<n;i++){
	       if(arr[i]>max){
	           s_max = max;
	           max = arr[i];
	       }
	       else if(arr[i]>s_max && arr[i]<max){
	           s_max = arr[i];
	       }
	   }

	   if(s_max == INT_MIN)
	    return -1;
	   return s_max;
	}
};

```

## Complexity Analysis:

### Time Complexity: O(N)

### Space Complexity: O(1)
