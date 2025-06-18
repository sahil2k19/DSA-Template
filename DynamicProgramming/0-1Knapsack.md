# 0/1 Knapsack Problem

## 🔍 Problem Statement
You are given `n` items with weights `wt[i]` and values `val[i]`, and a maximum weight capacity `W`.  
Your task is to determine the **maximum total value** that can be obtained by selecting a subset of the items such that their total weight does not exceed `W`.

Each item can be selected **at most once** (hence 0/1).

---

## 🧠 Recursion + Memoization (Top-Down DP)

### 🧾 Base Case
- If `i == 0`, only one item to consider:
  - If `wt[0] <= W` → return `val[0]`
  - Else return `0`

### 🛠️ C++ Code
```cpp
#include <bits/stdc++.h>
using namespace std;

int knapsack(int i, int W, vector<int>& wt, vector<int>& val, vector<vector<int>>& dp) {
    if (i == 0) {
        if (wt[0] <= W) return val[0];
        return 0;
    }

    if (dp[i][W] != -1) return dp[i][W];

    int notTake = knapsack(i - 1, W, wt, val, dp);
    int take = INT_MIN;
    if (wt[i] <= W)
        take = val[i] + knapsack(i - 1, W - wt[i], wt, val, dp);

    return dp[i][W] = max(take, notTake);
}

int main() {
    int n = 4, W = 8;
    vector<int> wt = {3, 4, 5, 6};
    vector<int> val = {2, 3, 4, 5};
    vector<vector<int>> dp(n, vector<int>(W + 1, -1));
    cout << "Max Profit: " << knapsack(n - 1, W, wt, val, dp);
}
