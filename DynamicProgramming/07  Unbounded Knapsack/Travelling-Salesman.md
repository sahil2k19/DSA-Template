# Travelling Salesman (Bitmask DP)

## 1. Problem Statement
Given an undirected weighted complete graph of `n` nodes (0..n-1), find the minimum cost to start at node 0, visit every node exactly once, and return to node 0.

## 2. Explain Approach (in short)
DP state `dp[mask][i]` = minimum cost to reach node `i` having visited nodes in `mask`. Transition by extending with new node `j`:
```
dp[mask | (1<<j)][j] = min(dp[mask][i] + cost[i][j])
```

## 3. Pseudocode with TC/SC
```cpp
function tsp(mask, i):
    if mask == (1<<n)-1:
        return cost[i][0]  // return to start
    if dp[mask][i] != INF:
        return dp[mask][i]
    ans = INF
    for j in 0…n-1:
        if not (mask & (1<<j)):
            ans = min(ans, cost[i][j] + tsp(mask | (1<<j), j))
    dp[mask][i] = ans
    return ans
return tsp(1<<0, 0)
// Time Complexity: O(n × 2^n)
// Space Complexity: O(n × 2^n)
```

## 4. Recursive Memoization Code with TC/SC
```cpp
#include <bits/stdc++.h>
using namespace std;
const int MAXN = 20;
const int INF = 1e9;
int n;
int cost[MAXN][MAXN];
int dp[1<<MAXN][MAXN];

int tsp(int mask, int pos) {
    if (mask == (1<<n) - 1)
        return cost[pos][0];
    int &ans = dp[mask][pos];
    if (ans != -1) return ans;
    ans = INF;
    for (int city = 0; city < n; ++city) {
        if (!(mask & (1<<city))) {
            ans = min(ans, cost[pos][city] + tsp(mask | (1<<city), city));
        }
    }
    return ans;
}

int main() {
    cin >> n;
    for (int i = 0; i < n; ++i)
        for (int j = 0; j < n; ++j)
            cin >> cost[i][j];
    memset(dp, -1, sizeof(dp));
    cout << tsp(1, 0) << endl;
    return 0;
}
// Time Complexity: O(n × 2^n)
// Space Complexity: O(n × 2^n)
```

## 5. Iteration (Tabulation) Code with TC/SC
```cpp
#include <bits/stdc++.h>
using namespace std;
const int INF = 1e9;

int main() {
    int n;
    cin >> n;
    vector<vector<int>> cost(n, vector<int>(n));
    for (int i = 0; i < n; ++i)
        for (int j = 0; j < n; ++j)
            cin >> cost[i][j];
    int N = 1 << n;
    vector<vector<int>> dp(N, vector<int>(n, INF));
    dp[1][0] = 0;
    for (int mask = 0; mask < N; ++mask) {
        for (int u = 0; u < n; ++u) {
            if (!(mask & (1 << u))) continue;
            for (int v = 0; v < n; ++v) {
                if (mask & (1 << v)) continue;
                dp[mask | (1 << v)][v] = min(
                    dp[mask | (1 << v)][v],
                    dp[mask][u] + cost[u][v]
                );
            }
        }
    }
    int res = INF;
    for (int u = 0; u < n; ++u) {
        res = min(res, dp[N-1][u] + cost[u][0]);
    }
    cout << res << endl;
    return 0;
}
// Time Complexity: O(n^2 × 2^n)
// Space Complexity: O(n × 2^n)
```

<!-- Save as Travelling-Salesman.md -->
