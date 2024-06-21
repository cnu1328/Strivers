# Alien Dictionary

[Problem Link](https://www.geeksforgeeks.org/problems/alien-dictionary/1)

## Approach - Using TopoSort

1. The main idea is to construct a graph based on the alien dictionary
2. To achive this, first construct a graph based on the strings that are given to us.
3. Check adjacent strigs character by character until the characters are not equal. 
4. If characters are not equal then push u -> v into graph
5. Example, 
    - abcd
    - abce
    - Here first three characters are equal,  the last characters are not equal, then 
    - mark d -> e, in graph
6. After this, implement toposort on constructed graph
    - find inDegree for each node
    - if inDegree of any node is zero, then push to the queue
    - Run a loop on queue, until it is empty
    - Everytime reduce the inDegree of its child nodes or adjatancy nodes, if there inDegree become zero, push into the queue
    - Finally toposort gives us the order for alien alphabets


**Follow Up Question - What If The order may not possible**
1. The order is not possible if
    - The first string's length is greater than second string in the array and the prefix characters are equal
    - arr[0] = abcde
    - arr[1] = abcdef
    - If above is there, the order not possible

2. The Order is not possible if
    - In the graph there exists cyclic dependency


```Java


class Solution{
    
    public:
    string findOrder(string dict[], int N, int K) {
        
        vector<int> graph[K];
        
        for(int i=0; i<N-1; i++) {
            string s1 = dict[i];
            string s2 = dict[i+1];
            
            int len = min(s1.length(), s2.length());
            
            for(int ii=0; ii<len; ii++) {
                if(s1[ii] != s2[ii]) {
                    graph[s1[ii] - 'a'].push_back(s2[ii] - 'a');
                    break;
                }
                
            }
        }
        
        int inDegree[K] = {0};
        
        for(int node = 0; node < K; node++) {
            
            for(int child : graph[node]) {
                inDegree[child]++;
            }
        }
        
        
        queue<int> que;
        
        for(int i=0; i<K; i++) {
            if(inDegree[i] == 0) que.push(i);
        }
        
        string ans = "";
        
        while(!que.empty()) {
            int node = que.front();
            ans += ('a' + node);
            que.pop();
            
            for(int child : graph[node]) {
                inDegree[child]--;
                
                if(inDegree[child] == 0) {
                    que.push(child);
                }
            }
        }
        
        // cout<<ans<<endl;
        
        return ans;
    }
};


```


## Complexity Analysis:

### Time Complexity: O(N*M)(m is maximum length of string) +  (K + E)

### Space Complexity: (K)