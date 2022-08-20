# Leacture 47
Problem : Number of Longest Increasing Subsequences (Code Studio)

Problem link : https://bit.ly/3fTRGiz

## 1) Using Memoization 
- LIS Approch

```C++
#include<bits/stdc++.h>
int findNumberOfLIS(vector<int> &arr)
{
    int n = arr.size();
    vector<int> dp(n,1),cnt(n,1);
    int mx = 1;
    for(int ind =0; ind<n;ind++)
    {
        for(int prev = 0;prev <ind; prev++)
        {
            if(arr[ind] > arr[prev] && 1 + dp[prev] > dp[ind])
            {
                dp[ind] = 1 + dp[prev];
                cnt[ind] = cnt[prev];
            }
            else if(arr[ind] > arr[prev] && 1 + dp[prev] == dp[ind])
            {
                cnt[ind] += cnt[prev];
            }
        }
        mx = max(mx,dp[ind]);
    }
    
    int no_lis = 0;
    for(int i =0;i<n;i++)
    {
        if(dp[i] == mx)
            no_lis += cnt[i];
    }
    return no_lis;
}
```
