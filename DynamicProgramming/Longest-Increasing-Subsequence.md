
# Longest Increasing Subsequence (LIS)

## 1. Problem Statement
Given an array `arr[]` of length `n`, find the length of the longest strictly increasing subsequence.

## 2. Explain Approach (in short)
Define `lis(i)` = LIS ending at `i`. Recursively consider all `j < i` with `arr[j] < arr[i]`. Use memo or 1D DP.

## 3. Pseudocode with TC/SC
```cpp
function lis(i):
    if i == 0: return 1
    maxLen = 1
    for j in 0…i-1:
        if arr[j] < arr[i]:
            maxLen = max(maxLen, lis(j) + 1)
    return maxLen

answer = max(lis(i) for i in 0…n-1)
Time Complexity: O(2ⁿ)
Space Complexity: O(n) (call stack)
```
## 4. Recursive Memoization Code with TC/SC
```cpp

#include <bits/stdc++.h>
using namespace std;

int lis(int i, const vector<int>& arr, vector<int>& dp) {
    if (dp[i] != -1) return dp[i];
    int mx = 1;
    for (int j = 0; j < i; j++) {
        if (arr[j] < arr[i])
            mx = max(mx, lis(j, arr, dp) + 1);
    }
    return dp[i] = mx;
}

int main() {
    int n; cin >> n;
    vector<int> arr(n);
    for (int &x : arr) cin >> x;
    vector<int> dp(n, -1);
    int ans = 0;
    for (int i = 0; i < n; i++)
        ans = max(ans, lis(i, arr, dp));
    cout << ans << "\n";
    return 0;
}
// TC: O(n²), SC: O(n²)
```
## 5. Iteration (Tabulation) Code with TC/SC
```cpp

#include <bits/stdc++.h>
using namespace std;

int lis_tab(const vector<int>& arr) {
    int n = arr.size();
    vector<int> dp(n, 1);
    int ans = 1;
    for (int i = 1; i < n; i++) {
        for (int j = 0; j < i; j++) {
            if (arr[j] < arr[i])
                dp[i] = max(dp[i], dp[j] + 1);
        }
        ans = max(ans, dp[i]);
    }
    return ans;
}

int main() {
    int n; cin >> n;
    vector<int> arr(n);
    for (int &x : arr) cin >> x;
    cout << lis_tab(arr) << "\n";
    return 0;
}
// TC: O(n²), SC: O(n)
```