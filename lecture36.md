# Leacture 36
Problem : Best Time to Buy and Sell Stock II (Code Studio)

Problem link : https://bit.ly/3nYO17H

## 1) Using Memoization 
- In this problem we have to calaculate max profit while we can buy and sell stock, we can again buy stock when we sell previous one.
- First we create dp grid of size nx2.(changing parameter are index and bay/sell).
- If we have to bay, we have two choices, buy this stock or not,We have to take max of bay it or not buy it.
- If we have to sell, we have two choices, sell this stock or not,We have to take max of sell it or not sell it.
- Return profit.

```C++
#include<bits/stdc++.h>
long fun(int ind,int buy,long *values, int n,vector<vector<long>> &dp)
{
    if(ind == n) return 0;
    
    if(dp[ind][buy] != -1) return dp[ind][buy];
    long profit = 0;
    
    if(buy)
    {
        profit = max(-values[ind] + fun(ind+1,0,values, n,dp),0 + fun(ind+1,1,values, n,dp));
    }
    else
    {
        profit = max(values[ind] + fun(ind+1,1,values, n,dp),0 + fun(ind+1,0,values, n,dp));
    }
    return dp[ind][buy] = profit;
}

long getMaximumProfit(long *values, int n)
{
    vector<vector<long>> dp(n,vector<long>(2,-1));
    
    return fun(0,1,values, n,dp);
}
```

## 2) Using Tabulation

```C++
 long getMaximumProfit(long *values, int n)
{
    vector<vector<long>> dp(n+1,vector<long>(2,0));
    
    dp[n][0] = dp[n][1] = 0;
    
    for(int ind = n-1;ind>=0; ind--)
    {
        for(int buy=0;buy<=1;buy++)
        {
            long profit = 0;
    
           if(buy)
           {
              profit = max(-values[ind] + dp[ind+1][0],0 + dp[ind+1][1]);
           }
           else
           {
              profit = max(values[ind] + dp[ind+1][1],0 + dp[ind+1][0]);
           }
           dp[ind][buy] = profit;
        }
    }
    return dp[0][1];
}
```

## 3) Using Space Optimization

```C++
long getMaximumProfit(long *values, int n)
{
    vector<long>ahead(2,0),curr(2,0);
    
    for(int ind = n-1;ind>=0; ind--)
    {
        for(int buy=0;buy<=1;buy++)
        {
            long profit = 0;
    
           if(buy)
           {
              profit = max(-values[ind] + ahead[0],0 + ahead[1]);
           }
           else
           {
              profit = max(values[ind] + ahead[1],0 + ahead[0]);
           }
           curr[buy] = profit;
        }
        ahead = curr;
    }
    return ahead[1];
}

```
