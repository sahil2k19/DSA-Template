
# Longest Palindromic Subsequence

## 1. Problem Statement
Given a string `s`, find the length of the longest subsequence of `s` that is also a palindrome.

## 2. Explain Approach (in short)
This is LCS between `s` and its reverse. Use a 2D DP table.

## 3. Pseudocode with TC/SC
```cpp
function lps(i,j):
    if i > j: return 0
    if i == j: return 1
    if s[i] == s[j]:
        return 2 + lps(i+1, j-1)
    return max(lps(i+1,j), lps(i,j-1))
Time: O(2ⁿ) | Space: O(n) (call stack)
```
## 4. Recursive Memoization Code with TC/SC
```cpp

#include <bits/stdc++.h>
using namespace std;
int lps(int i, int j, string& s, vector<vector<int>>& dp){
    if (i>j) return 0;
    if (i==j) return 1;
    if (dp[i][j]!=-1) return dp[i][j];
    if (s[i]==s[j])
        return dp[i][j]=2 + lps(i+1,j-1,s,dp);
    return dp[i][j]=max(lps(i+1,j,s,dp), lps(i,j-1,s,dp));
}
int main(){
    string s; cin>>s;
    int n=s.size();
    vector<vector<int>> dp(n, vector<int>(n, -1));
    cout<<lps(0,n-1,s,dp)<<"\n";
    return 0;
}
// TC: O(n²), SC: O(n²)
```
## 5. Iteration (Tabulation) Code with TC/SC
```cpp
#include <bits/stdc++.h>
using namespace std;
int lps_tab(string& s){
    int n=s.size();
    vector<vector<int>> dp(n, vector<int>(n,0));
    for(int i=n-1;i>=0;--i){
        dp[i][i]=1;
        for(int j=i+1;j<n;++j){
            if(s[i]==s[j])
                dp[i][j]=2+dp[i+1][j-1];
            else
                dp[i][j]=max(dp[i+1][j], dp[i][j-1]);
        }
    }
    return dp[0][n-1];
}
int main(){
    string s; cin>>s;
    cout<<lps_tab(s)<<"\n";
    return 0;
}
// TC: O(n²), SC: O(n²)
```