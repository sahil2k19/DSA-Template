
```markdown
<!-- 02_unbounded_knapsack.md -->
# Unbounded Knapsack

## Problem
Unlimited copies of each item.  Maximize value within capacity `W`.

## Tabulation
```cpp
vector<int> dp(W+1,0);
for(int i=0;i<n;++i)
  for(int w=wt[i];w<=W;++w)
    dp[w]=max(dp[w], val[i]+dp[w-wt[i]]);
