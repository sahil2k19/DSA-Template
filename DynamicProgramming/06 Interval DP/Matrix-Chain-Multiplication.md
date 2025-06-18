
# Matrix Chain Multiplication

## 1. Problem Statement
Given a chain of matrices with dimensions `p0×p1, p1×p2, …, p(n-1)×pn`, compute the minimum number of scalar multiplications to multiply the entire chain.

## 2. Explain Approach (in short)
Try all places to split chain; use 2D DP where `dp[i][j]` = min cost for multiplying matrices `i…j`.

## 3. Pseudocode with TC/SC
```cpp
function mcm(i, j):
    if i == j: return 0
    ans = ∞
    for k from i to j-1:
        cost = mcm(i,k) + mcm(k+1,j) + pi-1·pk·pj
        ans = min(ans, cost)
    return ans
return mcm(1, n)
Time: O(2ⁿ) | Space: O(n) (call stack)
```
## 4. Recursive Memoization Code with TC/SC
```cpp

#include <bits/stdc++.h>
using namespace std;
long long solve(int i, int j, vector<int>& p, vector<vector<long long>>& dp) {
    if (i == j) return 0;
    if (dp[i][j] != -1) return dp[i][j];
    long long ans = LLONG_MAX;
    for (int k = i; k < j; ++k) {
        long long cost = solve(i,k,p,dp)
                       + solve(k+1,j,p,dp)
                       + 1LL*p[i-1]*p[k]*p[j];
        ans = min(ans, cost);
    }
    return dp[i][j] = ans;
}
int main() {
    int n; cin >> n;
    vector<int> p(n+1);
    for (int &x : p) cin >> x;
    vector<vector<long long>> dp(n+1, vector<long long>(n+1, -1));
    cout << solve(1, n, p, dp) << "\n";
    return 0;
}
// TC: O(n³), SC: O(n²)
```
##5. Iteration (Tabulation) Code with TC/SC
```cpp

#include <bits/stdc++.h>
using namespace std;
long long mcm_tab(vector<int>& p) {
    int n = p.size()-1;
    vector<vector<long long>> dp(n+1, vector<long long>(n+1, 0));
    for (int len = 2; len <= n; ++len) {
        for (int i = 1; i+len-1 <= n; ++i) {
            int j = i+len-1;
            dp[i][j] = LLONG_MAX;
            for (int k = i; k < j; ++k) {
                dp[i][j] = min(dp[i][j],
                               dp[i][k] + dp[k+1][j] + 1LL*p[i-1]*p[k]*p[j]);
            }
        }
    }
    return dp[1][n];
}
int main() {
    int n; cin >> n;
    vector<int> p(n+1);
    for (int &x : p) cin >> x;
    cout << mcm_tab(p) << "\n";
    return 0;
}
// TC: O(n³), SC: O(n²)
```