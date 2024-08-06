# Page Faults in LRU

[Problem Link](https://www.geeksforgeeks.org/problems/page-faults-in-lru5603/1)

## Approach - 1

1. First we have been given the size of the frame,
2. Fill the values till the size of the map equals the frame size and increase the frame size.
3. Check every time, if the new processor, is exist or not exist, only increament the fault, if processor is not eixt
4. Find the minimum index and replace it with new processor if new processor is not exist in the map.
5. return total faults

```c++

class Solution{
public:
    int pageFaults(int n, int C, int pages[]){
        map<int, int> mp;
        int faults = 0;


        for(int i=0; i<n; i++) {
            if(mp.size() < C) {

                if(mp.find(pages[i]) == mp.end()) {
                    faults++;
                }

                mp[pages[i]] = i;
            }

            else {
                if(mp.find(pages[i]) == mp.end()) {

                    int mini = 1001;
                    int page = 0;

                    for(auto &it : mp) {
                        if(it.second < mini) {
                            mini = it.second;
                            page = it.first;
                        }
                    }

                    mp.erase(page);


                    faults++;
                }

                mp[pages[i]] = i;
            }
        }

        return faults;
    }
};


```

## Complexity Analysis:

### Time Complexity: O(N)

### Space Complexity: (N)
