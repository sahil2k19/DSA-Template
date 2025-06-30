
## Problem 2: Implement Lower Bound

### Problem Statement
Given a sorted array of `n` integers and a target value `x`, find the index of the **first element** that is **greater than or equal to `x`**. If all elements are smaller than `x`, return `n` (i.e., position where `x` can be inserted).

### Hint
Use a modified binary search to keep track of the potential answer while narrowing the search space. Even when you find a valid candidate, continue searching in the left half to find the first occurrence.

### C++ Pseudocode
```cpp
function lowerBound(arr, n, x):
    low = 0
    high = n
    ans = n
    while low < high:
        mid = (low + high) / 2
        if arr[mid] >= x:
            ans = mid
            high = mid
        else:
            low = mid + 1
    return ans
```

### Time Complexity
- Worst Case: O(log n)

### Space Complexity
- O(1)

---

### C++ Real Code
```cpp
#include <iostream>
using namespace std;

int lowerBound(int arr[], int n, int x) {
    int low = 0, high = n, ans = n;
    while (low < high) {
        int mid = low + (high - low) / 2;
        if (arr[mid] >= x) {
            ans = mid;
            high = mid;
        } else {
            low = mid + 1;
        }
    }
    return ans;
}

int main() {
    int arr[] = {2, 4, 6, 6, 8, 10};
    int n = sizeof(arr) / sizeof(arr[0]);
    int x = 6;
    int result = lowerBound(arr, n, x);
    cout << "Lower bound index for " << x << " is " << result << endl;
    return 0;
}