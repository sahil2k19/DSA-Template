
# Longest Common Subsequence (LCS)

## 1. Problem Statement
Given two strings `X` (length m) and `Y` (length n), find the length of their longest common subsequence.

## 2. Explain Approach (in short)
If last characters match, 1 + LCS of prefixes; else max of dropping one char. Use a 2D DP `(m+1)×(n+1)`.

## 3. Pseudocode with TC/SC
```cpp
function lcs(i, j):
    if i == 0 or j == 0: return 0
    if X[i-1] == Y[j-1]:
        return 1 + lcs(i-1, j-1)
    else:
        return max(lcs(i-1, j), lcs(i, j-1))
return lcs(m, n)
Time Complexity: O(2^(m+n))
Space Complexity: O(m+n) (call stack)
```
## 4. Recursive Memoization Code with TC/SC
```cpp

#include <bits/stdc++.h>
using namespace std;

int lcs(int i, int j, const string& X, const string& Y, vector<vector<int>>& dp) {
    if (i == 0 || j == 0) return 0;
    if (dp[i][j] != -1) return dp[i][j];
    if (X[i-1] == Y[j-1])
        return dp[i][j] = 1 + lcs(i-1, j-1, X, Y, dp);
    return dp[i][j] = max(lcs(i-1, j, X, Y, dp), lcs(i, j-1, X, Y, dp));
}

int main() {
    string X, Y; cin >> X >> Y;
    int m = X.size(), n = Y.size();
    vector<vector<int>> dp(m+1, vector<int>(n+1, -1));
    cout << lcs(m, n, X, Y, dp) << "\n";
    return 0;
}
// TC: O(m·n), SC: O(m·n)

```
## 5. Iteration (Tabulation) Code with TC/SC
```cpp

#include <bits/stdc++.h>
using namespace std;

int lcs_tab(const string& X, const string& Y) {
    int m = X.size(), n = Y.size();
    vector<vector<int>> dp(m+1, vector<int>(n+1, 0));
    for (int i = 1; i <= m; i++) {
        for (int j = 1; j <= n; j++) {
            if (X[i-1] == Y[j-1])
                dp[i][j] = dp[i-1][j-1] + 1;
            else
                dp[i][j] = max(dp[i-1][j], dp[i][j-1]);
        }
    }
    return dp[m][n];
}

int main() {
    string X, Y; cin >> X >> Y;
    cout << lcs_tab(X, Y) << "\n";
    return 0;
}
// TC: O(m·n), SC: O(m·n)

```