
# Coin Change (Minimum Coins)

## 1. Problem Statement
Given coin denominations `coins[]` and a target `amount`, find the minimum number of coins needed to make up `amount`. Return `-1` if not possible.

## 2. Explain Approach (in short)
Try every coin by reducing the amount; optimize via memo or a 1D DP array of size `amount+1`.

## 3. Pseudocode with TC/SC

```cpp
function coinChange(amount):
    if amount == 0: return 0
    res = INF
    for coin in coins:
        if amount ≥ coin:
            sub = coinChange(amount - coin)
            if sub ≠ -1:
                res = min(res, sub + 1)
    return (res if res ≠ INF else -1)
Time Complexity: O(cⁿ) (c = #coins)
Space Complexity: O(amount)
```
## 4. Recursive Memoization Code with TC/SC
```cpp

#include <bits/stdc++.h>
using namespace std;

int coinChange(int amt, const vector<int>& coins, vector<int>& dp) {
    if (amt == 0) return 0;
    if (dp[amt] != -1) return dp[amt];
    int ans = INT_MAX;
    for (int c : coins) {
        if (amt >= c) {
            int sub = coinChange(amt - c, coins, dp);
            if (sub != -1) ans = min(ans, sub + 1);
        }
    }
    return dp[amt] = (ans == INT_MAX ? -1 : ans);
}

int main() {
    int amount, n; cin >> amount >> n;
    vector<int> coins(n);
    for (int &x : coins) cin >> x;
    vector<int> dp(amount+1, -1);
    cout << coinChange(amount, coins, dp) << "\n";
    return 0;
}
// TC: O(amount·c), SC: O(amount)
```

## 5. Iteration (Tabulation) Code with TC/SC
```cpp

#include <bits/stdc++.h>
using namespace std;

int coinChange_tab(const vector<int>& coins, int amount) {
    vector<int> dp(amount+1, INT_MAX);
    dp[0] = 0;
    for (int a = 1; a <= amount; a++) {
        for (int c : coins) {
            if (a >= c && dp[a-c] != INT_MAX)
                dp[a] = min(dp[a], dp[a-c] + 1);
        }
    }
    return dp[amount] == INT_MAX ? -1 : dp[amount];
}

int main() {
    int amount, n; cin >> amount >> n;
    vector<int> coins(n);
    for (int &x : coins) cin >> x;
    cout << coinChange_tab(coins, amount) << "\n";
    return 0;
}
// TC: O(amount·c), SC: O(amount)
```