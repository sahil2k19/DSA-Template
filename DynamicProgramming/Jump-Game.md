# Jump Game

## 1. Problem Statement
Given an array `nums` where each element indicates the maximum jump length at that position, determine if you can reach the last index from the first index.

## 2. Explain Approach (in short)
Track farthest reachable index. In DP, mark reachable and propagate. Naïve recursion tests all jumps.

## 3. Pseudocode with TC/SC
```cpp
function canJump(i):
    if i >= n-1: return true
    for step in 1…nums[i]:
        if canJump(i + step):
            return true
    return false
// Time Complexity: O(n²)
// Space Complexity: O(n) (call stack)
```

## 4. Recursive Memoization Code with TC/SC
```cpp
#include <bits/stdc++.h>
using namespace std;

bool canJumpMemo(int i, vector<int>& nums, vector<int>& dp) {
    int n = nums.size();
    if (i >= n-1) return true;
    if (dp[i] != -1) return dp[i];
    int furthest = min(n-1, i + nums[i]);
    for (int j = i+1; j <= furthest; ++j) {
        if (canJumpMemo(j, nums, dp))
            return dp[i] = 1;
    }
    return dp[i] = 0;
}

int main() {
    int n;
    cin >> n;
    vector<int> nums(n);
    for (int &x : nums) cin >> x;
    vector<int> dp(n, -1);
    cout << (canJumpMemo(0, nums, dp) ? "true\n" : "false\n");
    return 0;
}
// Time Complexity: O(n²)
// Space Complexity: O(n)
```