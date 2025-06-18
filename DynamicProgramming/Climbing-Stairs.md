
# Climbing Stairs

## 1. Problem Statement
You’re climbing a staircase of `n` steps. Each move, you can climb either 1 or 2 steps. In how many distinct ways can you reach the top?

## 2. Explain Approach (in short)
This is the Fibonacci recurrence: `ways[n] = ways[n-1] + ways[n-2]`. Solve with memo or bottom-up.

## 3. Pseudocode with TC/SC
```cpp
function climb(i):
    if i == 0: return 1
    if i == 1: return 1
    return climb(i-1) + climb(i-2)
Time: O(2ⁿ) | Space: O(n) (call stack)
```
## 4. Recursive Memoization Code with TC/SC
```cpp

#include <bits/stdc++.h>
using namespace std;
int climb(int i, vector<int>& dp) {
    if (i == 0 || i == 1) return 1;
    if (dp[i] != -1) return dp[i];
    return dp[i] = climb(i-1, dp) + climb(i-2, dp);
}
int main() {
    int n; cin >> n;
    vector<int> dp(n+1, -1);
    cout << climb(n, dp) << "\n";
    return 0;
}
// TC: O(n), SC: O(n)
```
## 5. Iteration (Tabulation) Code with TC/SC
```cpp

#include <bits/stdc++.h>
using namespace std;
int climb_tab(int n) {
    if (n <= 1) return 1;
    vector<int> dp(n+1);
    dp[0] = dp[1] = 1;
    for (int i = 2; i <= n; ++i)
        dp[i] = dp[i-1] + dp[i-2];
    return dp[n];
}
int main() {
    int n; cin >> n;
    cout << climb_tab(n) << "\n";
    return 0;
}
// TC: O(n), SC: O(n)

```