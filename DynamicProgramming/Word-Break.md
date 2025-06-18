# Word Break

## 1. Problem Statement
Given a string `s` and a dictionary `wordDict`, return `true` if `s` can be segmented into a space-separated sequence of dictionary words.

## 2. Explain Approach (in short)
At index `i`, try all words; if `s.substr(i, len) == word` and `f(i+len)` is true, mark `f(i)` = true. Memoize or use DP array.

## 3. Pseudocode with TC/SC
```cpp
function canBreak(i):
    if i == len(s): return true
    for word in wordDict:
        if s.substr(i, word.length) == word and canBreak(i + word.length):
            return true
    return false
// Time Complexity: O(n²·w)
// Space Complexity: O(n)
```

## 4. Recursive Memoization Code with TC/SC
```cpp
#include <bits/stdc++.h>
using namespace std;

bool wordBreakMemo(int i, string& s, unordered_set<string>& dict, vector<int>& dp) {
    if (i == s.size()) return true;
    if (dp[i] != -1) return dp[i];
    for (auto &w : dict) {
        int len = w.size();
        if (i + len <= s.size() && s.substr(i, len) == w && wordBreakMemo(i+len, s, dict, dp))
            return dp[i] = 1;
    }
    return dp[i] = 0;
}

int main() {
    string s;
    cin >> s;
    int n;
    cin >> n;
    unordered_set<string> dict;
    for (int i = 0; i < n; ++i) {
        string w;
        cin >> w;
        dict.insert(w);
    }
    vector<int> dp(s.size(), -1);
    cout << (wordBreakMemo(0, s, dict, dp) ? "true\n" : "false\n");
    return 0;
}
// Time Complexity: O(n²·w)
// Space Complexity: O(n)
```