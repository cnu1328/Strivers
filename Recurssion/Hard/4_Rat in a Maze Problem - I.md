# Rat in a Maze Problem - I

[Problem Link](https://www.geeksforgeeks.org/problems/rat-in-a-maze-problem/1)


## Approach

1. from a cell we can go to other call if the other cell value is one.
2. We allowed to go in four directions(up, right, down, left)
3. For every cell try to go in four directions until you reach cell (n-1,  n-1)
4. take care of visited cell

```Java

class Solution {
  public:
    
    void solve(int row, int col, int n, vector<vector<int>> &mat, string &curr, vector<string> &ans,
    int dir[], char ch[], vector<vector<int>> &visited) {
        
        if(row == n-1 && col == n-1) {
            ans.push_back(curr);
            return;
        }
        
        visited[row][col] = true;
    
        
        
        for(int i=0; i<4; i++) {
            int newR = row + dir[i];
            int newC = col + dir[i + 1];
            
            if(newR >=0 && newR <n && newC >=0 && newC <n && mat[newR][newC] == 1 && visited[newR][newC] == 0) {
                curr.push_back(ch[i]);
                solve(newR, newC, n, mat, curr, ans, dir, ch, visited);
                curr.pop_back();
            }
        }
        
        visited[row][col] = false;
        
    }
  
    vector<string> findPath(vector<vector<int>> &mat) {
        
        vector<string> ans;
        string curr = "";
        
        int n = mat.size();
        
        int dir[] = {-1, 0, 1, 0, -1};
        
        char ch[] = {'U', 'R', 'D', 'L'};
        
        vector<vector<int>> visited(n, vector<int> (n, 0));
        
        if(mat[0][0]) {
            solve(0, 0, n, mat, curr, ans, dir, ch, visited);
        }
        
        return ans;
        
    }
};


```

## Complexity Analysis

### Time Complexity: O(4^(m*n))

### Space Complexiy: O(m*n)
