# Unbounded Knapsack (Complete Knapsack)

## 1. Problem Statement  
Given `n` item types with weights `wt[i]` and values `val[i]`, and a knapsack capacity `W`, you may take **unlimited** copies of each item. Maximize the total value without exceeding capacity `W`.

## 2. Explain Approach (in short)  
At each capacity `c`, for each item `i` you can either take it (stay at `c - wt[i]` and add `val[i]`) or skip it. A 1D DP array `dp[c]` holds the max value for capacity `c`.  

## 3. Pseudocode with TC/SC  
```cpp
function unboundedKnapsack(wt[], val[], n, W):
    dp = array of size W+1, initialized to 0
    for c in 0…W:
        for i in 0…n-1:
            if wt[i] ≤ c:
                dp[c] = max(dp[c], dp[c - wt[i]] + val[i])
    return dp[W]
// Time Complexity: O(n·W)
// Space Complexity: O(W)
```

## 4. Recursive Memoization Code with TC/SC  
```cpp
#include <bits/stdc++.h>
using namespace std;

int solve(int c, vector<int>& wt, vector<int>& val, vector<int>& dp) {
    if (c == 0) return 0;
    if (dp[c] != -1) return dp[c];
    int best = 0;
    for (int i = 0; i < wt.size(); ++i) {
        if (wt[i] <= c)
            best = max(best, val[i] + solve(c - wt[i], wt, val, dp));
    }
    return dp[c] = best;
}

int main() {
    int n, W;
    cin >> n >> W;
    vector<int> wt(n), val(n);
    for (int i = 0; i < n; ++i) cin >> wt[i];
    for (int i = 0; i < n; ++i) cin >> val[i];
    vector<int> dp(W+1, -1);
    cout << solve(W, wt, val, dp) << "\n";
    return 0;
}
// Time Complexity: O(n·W)
// Space Complexity: O(W + recursion stack)
```

## 5. Iteration (Tabulation) Code with TC/SC  
```cpp
#include <bits/stdc++.h>
using namespace std;

int unboundedKnapsack(vector<int>& wt, vector<int>& val, int W) {
    int n = wt.size();
    vector<int> dp(W+1, 0);
    for (int c = 0; c <= W; ++c) {
        for (int i = 0; i < n; ++i) {
            if (wt[i] <= c)
                dp[c] = max(dp[c], dp[c - wt[i]] + val[i]);
        }
    }
    return dp[W];
}

int main() {
    int n, W;
    cin >> n >> W;
    vector<int> wt(n), val(n);
    for (int i = 0; i < n; ++i) cin >> wt[i];
    for (int i = 0; i < n; ++i) cin >> val[i];
    cout << unboundedKnapsack(wt, val, W) << "\n";
    return 0;
}
// Time Complexity: O(n·W)
// Space Complexity: O(W)
```

<!-- You can save this as `Unbounded-Knapsack.md` and upload to Canvas -->
