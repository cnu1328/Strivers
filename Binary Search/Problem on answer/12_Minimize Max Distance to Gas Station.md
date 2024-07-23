# Minimize Max Distance to Gas Station

[Problem Link](https://www.geeksforgeeks.org/problems/minimize-max-distance-to-gas-station/1)

## Approach - 1 - Brute Force Approach

1. As we have to place the K Stations in between the existing stations to minimize the maximum distances.
2. Let's take an example arr = [1, 7] and K = 2
   - the difference between arr[0] - arr[1] = 6
   - If we place K stations in the between the 1 and 7, then the distance between them equals to (6 / (2 + 1)) => 2
   - From above we can observe that, to minimize the maximum distance, we need to place the new gas stations in the middle of the exising two stations
   - `distance/(number of stations placed + 1)` will give us the maximum distance, from all the distance we can find the minimum
3. For K gas stations find the maximum difference and insert the gas station in middle of them. Do the same process till we place all the gas stations
4. Then find the max distance between two gas stations

```Java

public static double minimiseMaxDistance(int[] arr, int k) {
    int n = arr.length; //size of array.
    int[] howMany = new int[n - 1];

    //Pick and place k gas stations:
    for (int gasStations = 1; gasStations <= k; gasStations++) {
        //Find the maximum section
        //and insert the gas station:
        double maxSection = -1;
        int maxInd = -1;
        for (int i = 0; i < n - 1; i++) {
            double diff = arr[i + 1] - arr[i];
            double sectionLength =
                diff / (double)(howMany[i] + 1);
            if (sectionLength > maxSection) {
                maxSection = sectionLength;
                maxInd = i;
            }
        }
        //insert the current gas station:
        howMany[maxInd]++;
    }

    //Find the maximum distance i.e. the answer:
    double maxAns = -1;
    for (int i = 0; i < n - 1; i++) {
        double diff = arr[i + 1] - arr[i];
        double sectionLength =
            diff / (double)(howMany[i] + 1);
        maxAns = Math.max(maxAns, sectionLength);
    }
    return maxAns;
}
```

## Complexity Analysis:

### Time Complexity: O(N \* K)

### Space Complexity: O(N)

## Approach - 2 - Using Priority Queue

1. Use priority queue, to get the maximum distance for every new gas station.
2. We can simply place the gas station between them

```Java

import java.util.*;

public class tUf {
    public static class Pair {
        double first;
        int second;

        Pair(double first, int second) {
            this.first = first;
            this.second = second;
        }
    }

    public static double minimiseMaxDistance(int[] arr, int k) {
        int n = arr.length; // size of array.
        int[] howMany = new int[n - 1];
        PriorityQueue<Pair> pq = new PriorityQueue<>((a, b) -> Double.compare(b.first, a.first));

        // insert the first n-1 elements into pq
        // with respective distance values:
        for (int i = 0; i < n - 1; i++) {
            pq.add(new Pair(arr[i + 1] - arr[i], i));
        }

        // Pick and place k gas stations:
        for (int gasStations = 1; gasStations <= k; gasStations++) {
            // Find the maximum section
            // and insert the gas station:
            Pair tp = pq.poll();
            int secInd = tp.second;

            // insert the current gas station:
            howMany[secInd]++;

            double inidiff = arr[secInd + 1] - arr[secInd];
            double newSecLen = inidiff / (double) (howMany[secInd] + 1);
            pq.add(new Pair(newSecLen, secInd));
        }

        return pq.peek().first;
    }

    public static void main(String[] args) {
        int[] arr = {1, 2, 3, 4, 5};
        int k = 4;
        double ans = minimiseMaxDistance(arr, k);
        System.out.println("The answer is: " + ans);
    }
}

```

## Complexity Analysis:

### Time Complexity: O(N log N \* K Log N)

### Space Complexity: O(N)

## Approach - 3 - Binary Search
