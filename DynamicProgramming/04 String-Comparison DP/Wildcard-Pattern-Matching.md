# Wildcard Pattern Matching

## 1. Problem Statement
Given an input string `s` and a pattern `p` containing `?` (matches any single character) and `*` (matches any sequence of characters), implement wildcard matching.

## 2. Explain Approach (in short)
Define `dp[i][j]` = whether `s[0..i-1]` matches `p[0..j-1]`. Handle `*` by matching zero or more chars, `?` or exact match by checking diagonal.

## 3. Pseudocode with TC/SC
```cpp
dp[0][0] = true
for j in 1…m:
    if p[j-1]=='*': dp[0][j] = dp[0][j-1]
for i in 1…n:
    for j in 1…m:
        if p[j-1]=='*'
            dp[i][j] = dp[i][j-1] || dp[i-1][j]
        else if p[j-1]=='?' || s[i-1]==p[j-1]
            dp[i][j] = dp[i-1][j-1]
// Time Complexity: O(n·m)
// Space Complexity: O(n·m)
```

## 4. Recursive Memoization Code with TC/SC
```cpp
#include <bits/stdc++.h>
using namespace std;

string s, p;
vector<vector<int>> dp;

bool matchMemo(int i, int j) {
    if (i==0 && j==0) return true;
    if (j==0) return false;
    if (dp[i][j] != -1) return dp[i][j];
    if (p[j-1] == '*') {
        bool skip = matchMemo(i, j-1);
        bool use  = (i>0) && matchMemo(i-1, j);
        return dp[i][j] = skip || use;
    }
    if (i>0 && (p[j-1]=='?' || s[i-1]==p[j-1]))
        return dp[i][j] = matchMemo(i-1, j-1);
    return dp[i][j] = false;
}

int main(){
    cin >> s >> p;
    int n = s.size(), m = p.size();
    dp.assign(n+1, vector<int>(m+1, -1));
    cout << (matchMemo(n, m) ? "true\n" : "false\n");
    return 0;
}
// Time Complexity: O(n·m)
// Space Complexity: O(n·m)
```