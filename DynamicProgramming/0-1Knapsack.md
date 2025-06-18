
# 0/1 Knapsack Problem

## 1. Problem Statement
Given weights `wt[]`, values `val[]` of `n` items and capacity `W`, select a subset to maximize total value without exceeding `W`. Each item can be chosen at most once.

## 2. Explain Approach (in short)
Decide for each item to include or skip. Use memoization or a DP table of size `(n+1)×(W+1)` for O(n·W).

## 3. Pseudocode with TC/SC
```cpp
function knap(i, W):
    if i == 0 or W == 0: return 0
    if wt[i-1] ≤ W:
        return max(val[i-1] + knap(i-1, W-wt[i-1]), knap(i-1, W))
    else:
        return knap(i-1, W)
return knap(n, W)
Time Complexity: O(2ⁿ)
Space Complexity: O(n) (call stack)
```
## 4. Recursive Memoization Code with TC/SC
```cpp
#include <bits/stdc++.h>
using namespace std;

int knap(int i, int W, const vector<int>& wt, const vector<int>& val, vector<vector<int>>& dp) {
    if (i == 0 || W == 0) return 0;
    if (dp[i][W] != -1) return dp[i][W];
    int without = knap(i-1, W, wt, val, dp);
    int with = (wt[i-1] <= W)
        ? val[i-1] + knap(i-1, W - wt[i-1], wt, val, dp)
        : 0;
    return dp[i][W] = max(with, without);
}

int main() {
    int n, W; cin >> n >> W;
    vector<int> wt(n), val(n);
    for (int i = 0; i < n; i++) cin >> wt[i];
    for (int i = 0; i < n; i++) cin >> val[i];
    vector<vector<int>> dp(n+1, vector<int>(W+1, -1));
    cout << knap(n, W, wt, val, dp) << "\n";
    return 0;
}
// TC: O(n·W), SC: O(n·W)
```
## 5. Iteration (Tabulation) Code with TC/SC
```cpp
#include <bits/stdc++.h>
using namespace std;

int knap_tab(const vector<int>& wt, const vector<int>& val, int W) {
    int n = wt.size();
    vector<vector<int>> dp(n+1, vector<int>(W+1, 0));
    for (int i = 1; i <= n; i++) {
        for (int w = 1; w <= W; w++) {
            if (wt[i-1] <= w)
                dp[i][w] = max(val[i-1] + dp[i-1][w - wt[i-1]], dp[i-1][w]);
            else
                dp[i][w] = dp[i-1][w];
        }
    }
    return dp[n][W];
}

int main() {
    int n, W; cin >> n >> W;
    vector<int> wt(n), val(n);
    for (int i = 0; i < n; i++) cin >> wt[i];
    for (int i = 0; i < n; i++) cin >> val[i];
    cout << knap_tab(wt, val, W) << "\n";
    return 0;
}
// TC: O(n·W), SC: O(n·W)
```