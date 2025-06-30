## Problem 1: Binary Search to Find `x` in a Sorted Array

### Problem Statement
Given a sorted array of `n` integers and a target value `x`, return the index of `x` in the array using Binary Search. If `x` is not present in the array, return -1.

### Hint
Binary Search works by repeatedly dividing the search interval in half. Compare the target with the middle element:
- If equal, return the index
- If less, search the left half
- If greater, search the right half

Make sure to update your search boundaries accordingly.

### C++ Pseudocode
```cpp
function binarySearch(arr, n, x):
    low = 0
    high = n - 1
    while low <= high:
        mid = (low + high) / 2
        if arr[mid] == x:
            return mid
        else if arr[mid] < x:
            low = mid + 1
        else:
            high = mid - 1
    return -1
```

### Time Complexity
- Best Case: O(1) (if the middle element is the target)
- Worst Case: O(log n)

### Space Complexity
- O(1) (Iterative solution uses constant space)

---

### C++ Real Code
```cpp
#include <iostream>
using namespace std;

int binarySearch(int arr[], int n, int x) {
    int low = 0, high = n - 1;
    while (low <= high) {
        int mid = low + (high - low) / 2;
        if (arr[mid] == x)
            return mid;
        else if (arr[mid] < x)
            low = mid + 1;
        else
            high = mid - 1;
    }
    return -1;
}

int main() {
    int arr[] = {3, 4, 6, 7, 9, 12, 16, 17};
    int n = sizeof(arr) / sizeof(arr[0]);
    int x = 16;
    int result = binarySearch(arr, n, x);
    if (result != -1)
        cout << "Element found at index " << result << endl;
    else
        cout << "Element not found" << endl;
    return 0;
}
