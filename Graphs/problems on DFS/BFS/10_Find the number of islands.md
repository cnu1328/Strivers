# Find the number of islands 

[Problem Link](https://www.geeksforgeeks.org/problems/find-the-number-of-islands/1)

## Approach - 1
1. It is same like finding number of connected components
2. But, Here we are allowed to move in 8 directions
3. Traverse the matrix, if you find 1 in any cell then call dfs
4. The dfs will visits all 1's that are connected
5. meanwhile calling dfs, we increment the count of connected components
6. finally return the count

```Java

class Solution {
  private:
    void dfs(int row, int col, vector<vector<int>> &visited, vector<vector<char>> grid,
    int dx[], int dy[]) {
        
        visited[row][col] = 1;
        int n = grid.size();
        int m = grid[0].size();
        
        for(int i=0; i<8; i++) {
            int x = row + dx[i];
            int y = col + dy[i];
            
            if(x < 0 || x >= n || y < 0 || y >= m) continue;
            
            if(grid[x][y] == '1' && !visited[x][y])
                dfs(x, y, visited, grid, dx, dy);
        }
    }
    
  public:
  
    // Function to find the number of islands.
    int numIslands(vector<vector<char>>& grid) {
        // Code here
        
        int ans = 0;
        int n = grid.size();
        int m = grid[0].size();
        vector<vector<int>> visited(n, vector<int> (m, 0));
        
        int dx[] = {-1, 1, 0, 1, 1, -1, 0, -1};
        int dy[] = {0, -1, 1, 1, 0, 1, -1, -1};
        
        
        for(int i=0; i<n; i++) {
            for(int j=0; j<m; j++) {
                if(grid[i][j] == '1' && !visited[i][j]) {
                    ans++;
                    dfs(i, j, visited, grid, dx, dy);
                }
            }
        }
        
        return ans;
    }
};

```



## Complexity Analysis:

### Time Complexity: (N*M + N*M*9)

### Space Complexity: (N*M)