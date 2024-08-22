# Minimum Multiplications to reach End

[Problem Link](https://www.geeksforgeeks.org/problems/minimum-multiplications-to-reach-end/1)

## Approach - 1

1. Our Node value range is from 0 to 99999, as given the modulo of 100000
2. So, everytime we multiply with the elements of array gives new node, and plus one step used.
3. See the below image for better understanding

<img width="725" alt="image" src="https://github.com/user-attachments/assets/e655c8b5-34d8-4b8c-8fb4-be4f7635474e">

4. Apply simple Dijskhra algorithm and return the answer

<img width="725" alt="image" src="https://github.com/user-attachments/assets/b209c901-8e3b-43d1-a399-920b5c328021">

```c++

class Solution {
  public:
    int mod = 1e5;

    int minimumMultiplications(vector<int>& arr, int start, int end) {

        queue<pair<int, int>> que;

        vector<int> steps(1e5, 1e9);

        que.push({0, start});

        while(!que.empty()) {
            int step = que.front().first;
            int node = que.front().second;

            que.pop();

            if(node == end) return step;

            for(int ele : arr) {
                int newNode = (node * ele)%mod;

                if(step + 1 < steps[newNode]) {
                    steps[newNode] = step + 1;

                    que.push({step + 1, newNode});
                }
            }
        }

        return -1;
    }
};


```

## Complexitiy Analysis:

### Time Complexity : O(100000 \* N)

### Space Compleixty : O(100000)
