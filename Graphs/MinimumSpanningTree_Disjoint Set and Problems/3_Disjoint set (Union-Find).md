# Disjoint set (Union-Find)

[Problem Link](https://www.geeksforgeeks.org/problems/disjoint-set-union-find/1)

## Disjoint set (Union-Find)

1. The main functionalities of Disjoint set are
   - Find Parent
   - Union - it can be achieved by two ways(union by rank and union by size)
2. The Use case of Disjoint set is

   - Does 1 & 4 belongs to same component
   - To determine using DFS/BFS it takes O(V + E)
   - Using Disjoint set it can be determined in constant time complexity
   - And we can easily tell that 1 & 4 belongs or not belongs to a component at any instance of iteration.

3. **Dynamic graph**: A dynamic graph generally refers to a graph that keeps on changing its configuration

   - After any step, if we try to figure out whether two arbitrary nodes u and v belong to the same component or not, Disjoint Set will be able to answer this query in constant time.

![image](https://github.com/user-attachments/assets/4b57f09c-4ea7-47de-8a7a-24d7314cfbf0)

4. **Rank**: The rank of a node generally refers to the distance (the number of nodes including the leaf node) between the furthest leaf node and the current node. Basically rank includes all the nodes beneath the current node.

![image](https://github.com/user-attachments/assets/b4f0fca6-efa1-41c4-8377-9659224e0e8d)

5. **Ultimate parent**: The parent of a node generally refers to the node right above that particular node. But the ultimate parent refers to the topmost node or the root node.

![image](https://github.com/user-attachments/assets/6e9e5e1e-63c0-45c6-a2c7-3e1476b4a021)

## Approach - 1 - Union By Rank

1. First we require the rank and parent arrays

   - Initial Configuration
     ![image](https://github.com/user-attachments/assets/9a4246cc-e365-42fb-80ef-814927e7c242)

2. Union(u, v)

   - Find the altimate parent of u and v as `pu` and `pv`
   - Find rank of pu and pv
   - Connect smaller rank to larger rank always

3. **why we need to find the ultimate parents:**

   - After union by rank operations, if we are asked (refer to the above picture) if node 5 and node 7 belong to the same component or not, the answer must be yes.
   - If we carefully look at their immediate parents, they are not the same but if we consider their ultimate parents they are the same i.e. node 4.
   - So, we can determine the answer by considering the ultimate parent.
   - That is why we need to find the ultimate parent.

4. **What is path compression?**

   - Basically, connecting each node in a particular path to its ultimate parent refers to path compression.

![image](https://github.com/user-attachments/assets/82f81522-94ee-4ba7-bbac-815f97c9d8c4)

5. **How the time complexity reduces**:

![image](https://github.com/user-attachments/assets/18627942-fd1a-43f7-b522-94625854fc5c)

6. **Note**: We cannot change the ranks while applying path compression.

7. **Follow-up question:**

   - Case 1
     ![image](https://github.com/user-attachments/assets/b123e207-fd66-4198-afa3-7d7c20b8b06c)

   - Case 2
     ![image](https://github.com/user-attachments/assets/756539e0-14d7-4d27-966c-995a672fcf11)

   - **shrinking the height of the graph.**
   - **reducing the time complexity as much as we can.**

```c++

#include<bits/stdc++.h>

using namespace std;

class DisjointSet {
    vector<int> parent, rank;
public:

    DisjointSet(int n) {

        rank.resize(n+1, 0);
        parent.resize(n+1);

        for(int i=0; i<=n; i++) {
            parent[i] = i;
        }
    }

    int findParent(int node) {
        if(node == parent[node]) {
            return node;
        }

        //return findParent(parent[node]);
        // with out path Compress, it takes O(Log N)
        // With path compress we get parent of a node in constant time

        // Path compress

        return parent[node] = findParent(parent[node]);
    }

    void unionByRank(int u, int v) {
        int pu = findParent(u);
        int pv = findParent(v);

        if(pu == pv) return;

        if(rank[pu] > rank[pv]) {
            parent[pu] = pv;
        }

        else if(rank[pu] < rank[pv]) {
            parent[pv] = pu;
        }

        else {
            parent[pv] = pu;
            rank[pv] ++;
        }
    }

};

int main() {
    DisjointSet ds(7);
    ds.unionByRank(1, 2);
    ds.unionByRank(2, 3);
    ds.unionByRank(4, 5);
    ds.unionByRank(6, 7);
    ds.unionByRank(5, 6);

    // if 3 and 7 are in same componet

    if(ds.findParent(3) == ds.findParent(7)) {
        cout<<"Same Parent"<<endl;
    }

    else cout<<"Not Same Parent"<<endl;

    ds.unionByRank(3, 7);

    if(ds.findParent(3) == ds.findParent(7)) {
        cout<<"Same Parent"<<endl;
    }

    else cout<<"Not Same Parent"<<endl;

}

```

```c++

// GFG

int find(int a[],int x)
{
    if(x == a[x]) return x;

    return find(a, a[x]);
}
void unionSet(int a[],int u,int v)
{
	int pu = find(a, u);
	int pv = find(a, v);

	if(pu == pv) return;

	a[pu] = pv;
}

```

## Complexitiy Analysis:

### Time Complexity : O(4 alpha)

### Space Compleixty : O(N)

- Until now, we have learned union by rank, the findPar() function, and the path compression technique.
- Now, if we again carefully observe, after applying path compression the rank of the graphs becomes distorted.
- So, rather than storing the rank, we can just store the size of the components for comparing which component is greater or smaller.

## Approach - 2 - Union By Size

1. This is as same as the Union by rank method except this method uses the size to compare the components while connecting.
2. That is why we need a ‘size’ array of size N(no. of nodes) instead of a rank array.
3. The size array will be storing the size for each particular node i.e. size[i] will be the size of the component starting from node i.

_Typically, the size of a node refers to the number of nodes that are connected to it._

```c++

#include<bits/stdc++.h>

using namespace std;

class DisjointSet {
    vector<int> parent, size;

public:

    DisjointSet(int n) {

        size.resize(n+1, 1);

        parent.resize(n+1);

        for(int i=0; i<=n; i++) {
            parent[i] = i;
        }
    }

    int findParent(int node) {
        if(node == parent[node]) return node;

        return parent[node] = findParent(parent[node]);
    }

    void unionBySize(int u, int v) {
        int pu = findParent(u);
        int pv = findParent(v);

        if(pu == pv) return;

        if(size[pu] < size[pv]) {
            parent[pu] = pv;
            size[pv] += size[pu];
        } else {
            parent[pv] = pu;
            size[pu] += size[pv];
        }
    }

};

int main() {

    DisjointSet ds(7);
    ds.unionBySize(1, 2);
    ds.unionBySize(2, 3);
    ds.unionBySize(4, 5);
    ds.unionBySize(6, 7);
    ds.unionBySize(5, 6);

    // if 3 and 7 are in same componet

    if(ds.findParent(3) == ds.findParent(7)) {
        cout<<"Same Parent"<<endl;
    }

    else cout<<"Not Same Parent"<<endl;

    ds.unionBySize(3, 7);

    if(ds.findParent(3) == ds.findParent(7)) {
        cout<<"Same Parent"<<endl;
    }

    else cout<<"Not Same Parent"<<endl;
}

```

## Complexitiy Analysis:

### Time Complexity : O(4 alpha)

### Space Compleixty : O(N)
