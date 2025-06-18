# House Robber

## 1. Problem Statement
You are a professional robber planning to rob houses along a street. Each house has some amount of money. Adjacent houses have a security system connected, so you cannot rob two adjacent houses. Given an array `nums`, return the maximum amount you can rob.

## 2. Explain Approach (in short)
At each index `i`, choose to rob it (`nums[i] + f(i-2)`) or skip it (`f(i-1)`). Naïve recursion is exponential; use memoization or bottom-up DP to make it linear.

## 3. Pseudocode with TC/SC
```cpp
function rob(i):
    if i < 0: return 0
    return max(rob(i-1), rob(i-2) + nums[i])
return rob(n-1)
Time Complexity: O(2ⁿ)
Space Complexity: O(n) (call stack)
```
## 4. Recursive Memoization Code with TC/SC
```cpp

#include <bits/stdc++.h>
using namespace std;

int robMemo(int i, vector<int>& nums, vector<int>& dp) {
    if (i < 0) return 0;
    if (dp[i] != -1) return dp[i];
    int skip = robMemo(i-1, nums, dp);
    int take = nums[i] + robMemo(i-2, nums, dp);
    return dp[i] = max(skip, take);
}

int main() {
    int n; cin >> n;
    vector<int> nums(n);
    for (int &x : nums) cin >> x;
    vector<int> dp(n, -1);
    cout << robMemo(n-1, nums, dp) << "\n";
    return 0;
}
// TC: O(n), SC: O(n)
## 5. Iteration (Tabulation) Code with TC/SC
```cpp

#include <bits/stdc++.h>
using namespace std;

int robTab(vector<int>& nums) {
    int n = nums.size();
    if (n == 0) return 0;
    vector<int> dp(n+1);
    dp[0] = 0; 
    dp[1] = nums[0];
    for (int i = 2; i <= n; ++i) {
        dp[i] = max(dp[i-1], dp[i-2] + nums[i-1]);
    }
    return dp[n];
}

int main() {
    int n; cin >> n;
    vector<int> nums(n);
    for (int &x : nums) cin >> x;
    cout << robTab(nums) << "\n";
    return 0;
}
// TC: O(n), SC: O(n)
```