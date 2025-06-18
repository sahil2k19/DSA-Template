# Unique Paths

## 1. Problem Statement
Given a grid of size `m×n`, count the number of unique paths from the top-left corner to the bottom-right corner. You can only move right or down.

## 2. Explain Approach (in short)
At each cell `(i,j)`, the number of ways = ways from above + ways from left. Naïve recursion is exponential; DP makes it O(m·n).

## 3. Pseudocode with TC/SC
```cpp
function paths(i, j):
    if i == 0 || j == 0:
        return 1
    return paths(i-1, j) + paths(i, j-1)
// Time Complexity: O(2^(m+n))
// Space Complexity: O(m+n) (call stack)
```

## 4. Recursive Memoization Code with TC/SC
```cpp
#include <bits/stdc++.h>
using namespace std;

int uniquePathsMemo(int i, int j, vector<vector<int>>& dp) {
    if (i == 0 || j == 0) return 1;
    if (dp[i][j] != -1) return dp[i][j];
    return dp[i][j] = uniquePathsMemo(i-1, j, dp) + uniquePathsMemo(i, j-1, dp);
}

int main() {
    int m, n;
    cin >> m >> n;
    vector<vector<int>> dp(m, vector<int>(n, -1));
    cout << uniquePathsMemo(m-1, n-1, dp) << "\n";
    return 0;
}
// Time Complexity: O(m·n)
// Space Complexity: O(m·n)
```

## 5. Iteration (Tabulation) Code with TC/SC
```cpp
#include <bits/stdc++.h>
using namespace std;

int uniquePathsTab(int m, int n) {
    vector<vector<int>> dp(m, vector<int>(n, 1));
    for (int i = 1; i < m; ++i) {
        for (int j = 1; j < n; ++j) {
            dp[i][j] = dp[i-1][j] + dp[i][j-1];
        }
    }
    return dp[m-1][n-1];
}

int main() {
    int m, n;
    cin >> m >> n;
    cout << uniquePathsTab(m, n) << "\n";
    return 0;
}
// Time Complexity: O(m·n)
// Space Complexity: O(m·n)
```