# M-Coloring Problem

[Problem Link](https://www.geeksforgeeks.org/problems/m-coloring-problem-1587115620/1)

## Approach - 1

1. Start from vertex 0, and color one by one the other vertices
2. The base condition returns true if recurrssion reaches the index N
3. Try out all possible colors for a node like from 0 to m-1 colors
4. For every possible color, check if the color is possible to color a node
5. Use color hash to store the colorings of a node, which tells present color of a node(like in the recurssion path)
6. Then again call for next node, if any of the node returns true then return true from that recurssion call. Which stops further calls of recurssion. As the question is asking only can we color?
7. After every recurssion call, de-color the node with -1(no color)
8. If we cannot color a graph with M color's then return false

```Java

class Solution{
public:
    // Function to determine if graph can be coloured with at most M colours such
    // that no two adjacent vertices of graph are coloured with same colour.
    
    bool isPossible(int index, int currentColor, int n, bool graph[101][101], vector<int> &color) {
        
        for(int i=0; i<n; i++) {
            if(graph[index][i] == 1 && color[i] == currentColor) {
                return false;
            }
        }
        
        return true;
    }
    
    bool helper(int index, int m, int n, bool graph[101][101], vector<int> &color) {
        if(index == n) {
            return true;
        }
        
        for(int i=0; i<m; i++) {
            if(isPossible(index, i, n, graph, color)) {
                color[index] = i;
                if(helper(index + 1, m, n, graph, color) == true) {
                    return true;
                }
                
                color[index] = -1;
                
            }
        }
        
        return false;
        
        
    }
    
    bool graphColoring(bool graph[101][101], int m, int n) {
        
        vector<int> color(n, -1);
        
        return helper(0, m, n, graph, color);
    }
};


```

## Complexity Analysis

### Time Complexity: O(N^M)
### Space Complexity: O(N)