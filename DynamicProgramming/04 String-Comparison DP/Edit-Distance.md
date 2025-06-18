
# Edit Distance (Levenshtein)

## 1. Problem Statement
Given two strings `s` and `t`, find the minimum number of operations (insert, delete, replace) to convert `s` into `t`.

## 2. Explain Approach (in short)
At each pair `(i,j)`, consider cost of delete, insert, or replace. Use 2D DP of size `(m+1)×(n+1)`.

## 3. Pseudocode with TC/SC
```cpp
function ed(i,j):
    if i==0: return j
    if j==0: return i
    if s[i-1]==t[j-1]:
        return ed(i-1,j-1)
    return 1 + min(
        ed(i-1,j),    // delete
        ed(i,j-1),    // insert
        ed(i-1,j-1)   // replace
    )
Time: O(3^(m+n)) | Space: O(m+n)
```
## 4. Recursive Memoization Code with TC/SC
```cpp

#include <bits/stdc++.h>
using namespace std;
int ed(int i, int j, string& s, string& t, vector<vector<int>>& dp) {
    if (i==0) return j;
    if (j==0) return i;
    if (dp[i][j] != -1) return dp[i][j];
    if (s[i-1]==t[j-1])
        return dp[i][j] = ed(i-1,j-1,s,t,dp);
    return dp[i][j] = 1 + min({
        ed(i-1,j,  s,t,dp),
        ed(i,  j-1,s,t,dp),
        ed(i-1,j-1,s,t,dp)
    });
}
int main(){
    string s,t; cin>>s>>t;
    int m=s.size(), n=t.size();
    vector<vector<int>> dp(m+1, vector<int>(n+1, -1));
    cout<<ed(m,n,s,t,dp)<<"\n";
    return 0;
}
// TC: O(m·n), SC: O(m·n)
```
## 5. Iteration (Tabulation) Code with TC/SC
```cpp
Copy
Edit
#include <bits/stdc++.h>
using namespace std;
int ed_tab(string& s, string& t) {
    int m=s.size(), n=t.size();
    vector<vector<int>> dp(m+1, vector<int>(n+1));
    for (int i=0;i<=m;i++) dp[i][0]=i;
    for (int j=0;j<=n;j++) dp[0][j]=j;
    for (int i=1;i<=m;i++){
        for (int j=1;j<=n;j++){
            if (s[i-1]==t[j-1])
                dp[i][j]=dp[i-1][j-1];
            else
                dp[i][j]=1+min({dp[i-1][j],dp[i][j-1],dp[i-1][j-1]});
        }
    }
    return dp[m][n];
}
int main(){
    string s,t; cin>>s>>t;
    cout<<ed_tab(s,t)<<"\n";
    return 0;
}
// TC: O(m·n), SC: O(m·n)
```