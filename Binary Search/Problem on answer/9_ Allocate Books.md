# Allocate Books

[Problem Link](https://www.naukri.com/code360/problems/allocate-books_1090540)

## Approach - 1 - Brute Force

1. Our search space is lies in the range of [max(arr), sum(arr)]
2. For every element in the search space, check we can allocate m books with this maximum number of pages, return minimum out of all

```Java




import java.util.*;

public class Main {
    public static int countStudents(ArrayList<Integer> arr, int pages) {
        int n = arr.size(); // size of array
        int students = 1;
        long pagesStudent = 0;
        for (int i = 0; i < n; i++) {
            if (pagesStudent + arr.get(i) <= pages) {
                // add pages to current student
                pagesStudent += arr.get(i);
            } else {
                // add pages to next student
                students++;
                pagesStudent = arr.get(i);
            }
        }
        return students;
    }

    public static int findPages(ArrayList<Integer> arr, int n, int m) {
        // book allocation impossible
        if (m > n)
            return -1;

        int low = Collections.max(arr);
        int high = arr.stream().mapToInt(Integer::intValue).sum();

        for (int pages = low; pages <= high; pages++) {
            if (countStudents(arr, pages) == m) {
                return pages;
            }
        }
        return low;
    }

    public static void main(String[] args) {
        ArrayList<Integer> arr = new ArrayList<>(Arrays.asList(25, 46, 28, 49, 24));
        int n = 5;
        int m = 4;
        int ans = findPages(arr, n, m);
        System.out.println("The answer is: " + ans);
    }
}

```

## Complexity Analysis:

### Time Complexity: O(N \* X) where X = [max(arr), sum(arr)]

### Space Complexity: O(1)

## Approach 2

1. Instead of Linear traversal on the search space, just do binary search
2. For every mid, check if we can allocate the number of pages to greater than or equal to M students, then find the minimum out of all and eliminate the right side
3. other wise eliminate the left side
4. How do we know we can allocate books to M students
   - Traverse on the given array, initially `students = 0`, add the pages to the current student
   - If the number of pages(sum of pages `pages`) to the current student becomes grater than required pages(mid) then increment the students by 1 and and assign `pages` to current number of pages.
   - return the number of students
5. It is not possible to allocate the books to M students, when students are greater than the number of books

```java

int findCount(vector<int>& arr, int pages) {
    int student = 1, studentPages = 0;
    for(int i=0; i<arr.size(); i++) {
        if(studentPages + arr[i] <= pages) {
            studentPages += arr[i];
        }
        else {
            studentPages = arr[i];
            student++;
        }
    }
    return student;
}

int findPages(vector<int>& arr, int n, int m) {

    if(m > n) return -1;

    int low = *max_element(arr.begin(), arr.end());
    int high = accumulate(arr.begin(), arr.end(), 0);

    int ans = INT_MAX;

    while(low <= high) {
        int mid = (low + high) >> 1;

        int studentCount = findCount(arr, mid);

        if(studentCount <= m) {
            ans = min(ans, mid);
            high = mid - 1;
        }

        else {
            low = mid + 1;
        }
    }

    return ans;
}

```

## Complexity Analysis:

### Time Complexity: O(N \* Log X) where X = [max(arr), sum(arr)]

### Space Complexity: O(1)
