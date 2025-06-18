
# Fibonacci Sequence

## 1. Problem Statement
Given an integer `n`, compute the `n`th Fibonacci number, where  
fib(0) = 0
fib(1) = 1
fib(n) = fib(n-1) + fib(n-2)

vbnet
Copy
Edit

## 2. Explain Approach (in short)
Recursion has overlapping subproblems (O(2ⁿ)). Use memoization or bottom-up tabulation to reduce to O(n).

## 3. Pseudocode with TC/SC
```js
function fib(n):
    if n ≤ 1: return n
    return fib(n-1) + fib(n-2)
//Time Complexity: O(2ⁿ)
//Space Complexity: O(n) (call stack)
```

## 4. Recursive Memoization Code with TC/SC

```cpp
#include <bits/stdc++.h>
using namespace std;
using ll = long long;

ll fib(int n, vector<ll>& dp) {
    if (n <= 1) return n;
    if (dp[n] != -1) return dp[n];
    return dp[n] = fib(n-1, dp) + fib(n-2, dp);
}

int main() {
    int n; cin >> n;
    vector<ll> dp(n+1, -1);
    cout << fib(n, dp) << "\n";
    return 0;
}
// TC: O(n), SC: O(n)
```

## 5. Iteration (Tabulation) Code with TC/SC
```cpp
#include <bits/stdc++.h>
using namespace std;
using ll = long long;

ll fib_tab(int n) {
    if (n <= 1) return n;
    vector<ll> dp(n+1);
    dp[0] = 0; dp[1] = 1;
    for (int i = 2; i <= n; i++)
        dp[i] = dp[i-1] + dp[i-2];
    return dp[n];
}

int main() {
    int n; cin >> n;
    cout << fib_tab(n) << "\n";
    return 0;
}
// TC: O(n), SC: O(n)