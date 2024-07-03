# Rat in a Maze Problem - I

[Problem Link](https://www.geeksforgeeks.org/problems/rat-in-a-maze-problem/1)


## Approach

1. from a cell we can go to other call if the other cell value is one.
2. We allowed to go in four directions(up, right, down, left)
3. For every cell try to go in four directions until you reach cell (n-1,  n-1)
4. take care of visited cell

```Java

// User function template for C++

class Solution{
    public:
    
    void solve(int row, int col, int n, vector<vector<int>> &m, string &curr, vector<string> &ans,
    int dx[], int dy[], char ch[], vector<vector<int>> &visited) {
        
        if(row == n-1 && col == n-1) {
            ans.push_back(curr);
            return;
        }
        
        
        for(int i=0; i<4; i++) {
            int newR = row + dx[i];
            int newC = col + dy[i];
            
            if(newR >=0 && newR <n && newC >=0 && newC <n && m[newR][newC] == 1 && visited[newR][newC] == 0) {
                curr.push_back(ch[i]);
                visited[newR][newC] = 1;
                solve(newR, newC, n, m, curr, ans, dx, dy, ch, visited);
                curr.pop_back();
                visited[newR][newC] = 0;
            }
        }
        
    }
    
    vector<string> findPath(vector<vector<int>> &m, int n) {
        // Your code goes here
        
        vector<string> ans;
        string curr = "";
        
        int dx[] = {-1, 1, 0, 0};
        int dy[] = {0, 0, 1, -1};
        
        char ch[] = {'U', 'D', 'R', 'L'};
        
        vector<vector<int>> visited(n, vector<int> (n, 0));
        
        visited[0][0] = 1;
        
        if(m[0][0]) {
            solve(0, 0, n, m, curr, ans, dx, dy, ch, visited);
        }
        
        return ans;
        
    }
};


```

## Complexity Analysis

### Time Complexity: O(4^(m*n))

### Space Complexiy: O(m*n)