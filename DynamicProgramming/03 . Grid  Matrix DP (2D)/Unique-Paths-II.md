# Unique Paths II

## 1. Problem Statement
Given an `m×n` grid with obstacles (1) and free cells (0), count unique paths from the top-left to the bottom-right. You can only move right or down.

## 2. Explain Approach (in short)
Same as Unique Paths but if a cell is blocked, ways = 0. Use DP with obstacle checks.

## 3. Pseudocode with TC/SC
```cpp
function paths(i, j):
    if i < 0 || j < 0 || grid[i][j] == 1:
        return 0
    if i == 0 && j == 0:
        return 1
    return paths(i-1, j) + paths(i, j-1)
// Time Complexity: O(2^(m+n))
// Space Complexity: O(m+n) (call stack)
```

## 4. Recursive Memoization Code with TC/SC
```cpp
#include <bits/stdc++.h>
using namespace std;

int uniquePaths2Memo(int i, int j, vector<vector<int>>& grid, vector<vector<int>>& dp) {
    if (i < 0 || j < 0 || grid[i][j] == 1) return 0;
    if (i == 0 && j == 0) return 1;
    if (dp[i][j] != -1) return dp[i][j];
    return dp[i][j] = uniquePaths2Memo(i-1, j, grid, dp)
                    + uniquePaths2Memo(i, j-1, grid, dp);
}

int main() {
    int m, n;
    cin >> m >> n;
    vector<vector<int>> grid(m, vector<int>(n));
    for (int i = 0; i < m; ++i)
        for (int j = 0; j < n; ++j)
            cin >> grid[i][j];
    vector<vector<int>> dp(m, vector<int>(n, -1));
    cout << uniquePaths2Memo(m-1, n-1, grid, dp) << "\n";
    return 0;
}
// Time Complexity: O(m·n)
// Space Complexity: O(m·n)
```

## 5. Iteration (Tabulation) Code with TC/SC
```cpp
#include <bits/stdc++.h>
using namespace std;

int uniquePaths2Tab(vector<vector<int>>& grid) {
    int m = grid.size(), n = grid[0].size();
    vector<vector<int>> dp(m, vector<int>(n, 0));
    if (grid[0][0] == 0) dp[0][0] = 1;
    for (int i = 1; i < m; ++i)
        if (grid[i][0] == 0) dp[i][0] = dp[i-1][0];
    for (int j = 1; j < n; ++j)
        if (grid[0][j] == 0) dp[0][j] = dp[0][j-1];
    for (int i = 1; i < m; ++i) {
        for (int j = 1; j < n; ++j) {
            if (grid[i][j] == 0)
                dp[i][j] = dp[i-1][j] + dp[i][j-1];
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
    cout << uniquePaths2Tab(grid) << "\n";
    return 0;
}
// Time Complexity: O(m·n)
// Space Complexity: O(m·n)
```