# Minimum Path Sum

## 1. Problem Statement
Given an `m×n` grid of non-negative numbers, find a path from the top-left to the bottom-right which minimizes the sum of all numbers along the path. You can only move down or right.

## 2. Explain Approach (in short)
DP where `dp[i][j] = grid[i][j] + min(dp[i-1][j], dp[i][j-1])`. Base edges handled separately.

## 3. Pseudocode with TC/SC
```cpp
function minSum(i, j):
    if i < 0 || j < 0:
        return INF
    if i == 0 && j == 0:
        return grid[0][0]
    return grid[i][j] + min(minSum(i-1, j), minSum(i, j-1))
// Time Complexity: O(2^(m+n))
// Space Complexity: O(m+n) (call stack)
```

## 4. Recursive Memoization Code with TC/SC
```cpp
#include <bits/stdc++.h>
using namespace std;

int minPathMemo(int i, int j, vector<vector<int>>& grid, vector<vector<int>>& dp) {
    if (i < 0 || j < 0) return INT_MAX;
    if (i == 0 && j == 0) return grid[0][0];
    if (dp[i][j] != -1) return dp[i][j];
    int up = minPathMemo(i-1, j, grid, dp);
    int left = minPathMemo(i, j-1, grid, dp);
    return dp[i][j] = grid[i][j] + min(up, left);
}

int main() {
    int m, n;
    cin >> m >> n;
    vector<vector<int>> grid(m, vector<int>(n));
    for (int i = 0; i < m; ++i)
        for (int j = 0; j < n; ++j)
            cin >> grid[i][j];
    vector<vector<int>> dp(m, vector<int>(n, -1));
    cout << minPathMemo(m-1, n-1, grid, dp) << "\n";
    return 0;
}
// Time Complexity: O(m·n)
// Space Complexity: O(m·n)
```

## 5. Iteration (Tabulation) Code with TC/SC
```cpp
#include <bits/stdc++.h>
using namespace std;

int minPathTab(vector<vector<int>>& grid) {
    int m = grid.size(), n = grid[0].size();
    vector<vector<int>> dp(m, vector<int>(n, 0));
    dp[0][0] = grid[0][0];
    for (int i = 1; i < m; ++i)
        dp[i][0] = dp[i-1][0] + grid[i][0];
    for (int j = 1; j < n; ++j)
        dp[0][j] = dp[0][j-1] + grid[0][j];
    for (int i = 1; i < m; ++i) {
        for (int j = 1; j < n; ++j) {
            dp[i][j] = grid[i][j] + min(dp[i-1][j], dp[i][j-1]);
        }
    }
    return dp[m-1][n-1];
}

int main() {
    int m, n;
    cin >> m >> n;
    vector<vector<int>> grid(m, vector<int>(n));
    for (int i = 0; i < m; ++i)
        for (int j = 0; j < n; ++j)
            cin >> grid[i][j];
    cout << minPathTab(grid) << "\n";
    return 0;
}
// Time Complexity: O(m·n)
// Space Complexity: O(m·n)
```