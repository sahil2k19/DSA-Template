# Palindromic Partitioning

## 1. Problem Statement
Given a string `s`, partition `s` such that every substring is a palindrome. Return the minimum number of cuts needed.

## 2. Explain Approach (in short)
Precompute a palindrome table. For index `i`, try every `j ≥ i` where `s[i..j]` is palindrome and recurse for `j+1`, adding one cut.

## 3. Pseudocode with TC/SC
```cpp
function minCut(i):
    if i == n: return -1
    ans = INF
    for j in i…n-1:
        if isPal[i][j]:
            ans = min(ans, 1 + minCut(j+1))
    return ans
// Time Complexity: exponential
// Space Complexity: O(n)
```

## 4. Recursive Memoization Code with TC/SC
```cpp
#include <bits/stdc++.h>
using namespace std;

string s;
vector<vector<bool>> pal;
vector<int> dp;

int minCutMemo(int i) {
    int n = s.size();
    if (i == n) return -1;
    if (dp[i] != -1) return dp[i];
    int ans = INT_MAX;
    for (int j = i; j < n; ++j) {
        if (pal[i][j]) {
            int cuts = 1 + minCutMemo(j+1);
            ans = min(ans, cuts);
        }
    }
    return dp[i] = ans;
}

int main() {
    getline(cin, s);
    int n = s.size();
    pal.assign(n, vector<bool>(n,false));
    for (int i = n-1; i >= 0; --i)
        for (int j = i; j < n; ++j)
            pal[i][j] = (s[i]==s[j]) && (j-i<2 || pal[i+1][j-1]);
    dp.assign(n, -1);
    cout << minCutMemo(0) << "\n";
    return 0;
}
// Time Complexity: O(n²)
// Space Complexity: O(n²)
```