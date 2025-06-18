
# Subset Sum

## 1. Problem Statement
Given an array `arr[]` and a target sum `S`, determine if there exists a subset of `arr` that adds up to `S`.

## 2. Explain Approach (in short)
Decision per element: include or exclude. Use a boolean DP table of size `(n+1)×(S+1)`.

## 3. Pseudocode with TC/SC
```cpp
function subset(i, sum):
    if sum == 0: return true
    if i == 0: return false
    if arr[i-1] ≤ sum:
        return subset(i-1, sum-arr[i-1]) OR subset(i-1, sum)
    else:
        return subset(i-1, sum)
Time: O(2ⁿ) | Space: O(n) (call stack)
```
## 4. Recursive Memoization Code with TC/SC

```cpp
#include <bits/stdc++.h>
using namespace std;
bool solve(int i, int sum, vector<int>& arr, vector<vector<int>>& dp) {
    if (sum == 0) return true;
    if (i == 0) return false;
    if (dp[i][sum] != -1) return dp[i][sum];
    bool pick = false;
    if (arr[i-1] <= sum)
        pick = solve(i-1, sum-arr[i-1], arr, dp);
    bool notPick = solve(i-1, sum, arr, dp);
    return dp[i][sum] = pick || notPick;
}
int main() {
    int n, S; cin >> n >> S;
    vector<int> arr(n);
    for (auto &x : arr) cin >> x;
    vector<vector<int>> dp(n+1, vector<int>(S+1, -1));
    cout << (solve(n, S, arr, dp) ? "YES\n" : "NO\n");
    return 0;
}
// TC: O(n·S), SC: O(n·S)
```
## 5. Iteration (Tabulation) Code with TC/SC
```cpp

#include <bits/stdc++.h>
using namespace std;
bool subset_tab(vector<int>& arr, int S) {
    int n = arr.size();
    vector<vector<bool>> dp(n+1, vector<bool>(S+1, false));
    for (int i = 0; i <= n; ++i) dp[i][0] = true;
    for (int i = 1; i <= n; ++i) {
        for (int s = 1; s <= S; ++s) {
            if (arr[i-1] <= s)
                dp[i][s] = dp[i-1][s-arr[i-1]] || dp[i-1][s];
            else
                dp[i][s] = dp[i-1][s];
        }
    }
    return dp[n][S];
}
int main() {
    int n, S; cin >> n >> S;
    vector<int> arr(n);
    for (auto &x : arr) cin >> x;
    cout << (subset_tab(arr, S) ? "YES\n" : "NO\n");
    return 0;
}
// TC: O(n·S), SC: O(n·S)