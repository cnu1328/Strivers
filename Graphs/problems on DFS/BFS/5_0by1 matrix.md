# 0/1 Matrix

[Problem Link](https://leetcode.com/problems/01-matrix/)


## Approach - 1 (TLE)

1. Find the minimum distance to 0 for every binary one
2. Use BFS-because, the adjacent cells are one distance from the centered cell

```Java

class Pair {
    int row;
    int col;
    int distance;
    
    Pair(int row, int col, int distance) {
        this.row= row;
        this.col = col;
        this.distance = distance;
    }
}

class Solution {
    
    private int bfs(int row, int col, int[][] mat) {
        
        int n = mat.length;
        int m = mat[0].length;
        
        int visited[][] = new int[n][m];
        
        Queue<Pair> queue = new LinkedList<>();
        
        queue.add(new Pair(row, col, 1));
        visited[row][col] = 1;
        
        int dx[] = {-1, 0, 1, 0};
        int dy[] = {0, 1, 0, -1};
        
        while(!queue.isEmpty()) {
            Pair pair = queue.poll();
            
            
            for(int i=0; i<4; i++) {
                int x = pair.row + dx[i];
                int y = pair.col + dy[i];
                
                if(x < 0 || x >= n || y < 0 || y >= m) continue;
                
                if(visited[x][y] == 0) {
                    if(mat[x][y] == 0) return pair.distance;
                    else {
                        visited[x][y] = 1;
                        queue.add(new Pair(x, y, pair.distance + 1));
                    }
                }
                        
            }
        }
        
        return 0;
        
        
    }
    
    public int[][] updateMatrix(int[][] mat) {
        
        int n = mat.length;
        int m = mat[0].length;
        
        int ans[][] = new int[n][m];
        
        
        for(int i=0; i<n; i++) {
            for(int j=0; j<m; j++) {
                
                if(mat[i][j] == 1) {
                    ans[i][j] = bfs(i, j, mat);
                }
                
                else ans[i][j] = mat[i][j];
            }
        }
        
        return ans;
    }
}

```

## Complexity Analysis:

### Time Complexity: O(N*M*(N*M)))

### Space Complexity: O(N*M)


## Approach - 1 - USING BFS

1. Calculated the distance for adjacent cells at once.

```Java

class Pair {
    int row;
    int col;
    int distance;
    
    Pair(int row, int col, int distance) {
        this.row= row;
        this.col = col;
        this.distance = distance;
    }
}

class Solution {
    
    
    public int[][] updateMatrix(int[][] mat) {
        
        int n = mat.length;
        int m = mat[0].length;
        
        int ans[][] = new int[n][m];
        boolean visited[][] = new boolean[n][m];
        
        Queue<Pair> queue = new LinkedList<>();
        
        for(int i=0; i<n; i++) {
            for(int j=0; j<m; j++) {
                if(mat[i][j] == 0) {
                    queue.add(new Pair(i, j, 0));
                    visited[i][j] = true;
                }
            }
        }
        
        int dx[] = {-1, 0, 1, 0};
        int dy[] = {0, 1, 0, -1};
        
        
        while(!queue.isEmpty()) {
            Pair pair = queue.poll();
            int row = pair.row;
            int col = pair.col;
            int dist = pair.distance;
            
            ans[row][col] = dist;
            
            for(int i=0; i<4; i++) {
                int x = row + dx[i];
                int y = col + dy[i];
                
                if(x < 0 || x>=n || y < 0 || y>=m) continue;
                
                if(!visited[x][y]) {
                    visited[x][y] = true;
                    queue.add(new Pair(x, y, dist + 1));
                }
            }
            
        }
        
        
        return ans;
        
        
    }
}

```

## Complexity Analysis:

### Time Complexity: O(N*M)

### Space Complexity: O(N*M)