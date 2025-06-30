## Problem 3: Implement Upper Bound

### Problem Statement
Given a sorted array of `n` integers and a target value `x`, find the index of the **first element that is strictly greater than `x`**. If all elements are less than or equal to `x`, return `n` (i.e., position where `x` would go if it were larger).

### Hint
Very similar to lower bound, but the condition checks for `arr[mid] > x` instead of `>=`.

### C++ Pseudocode
```cpp
function upperBound(arr, n, x):
    low = 0
    high = n
    ans = n
    while low < high:
        mid = (low + high) / 2
        if arr[mid] > x:
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

int upperBound(int arr[], int n, int x) {
    int low = 0, high = n, ans = n;
    while (low < high) {
        int mid = low + (high - low) / 2;
        if (arr[mid] > x) {
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
    int result = upperBound(arr, n, x);
    cout << "Upper bound index for " << x << " is " << result << endl;
    return 0;
}
```
