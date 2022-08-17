# Leacture 38
Problem : Best Time to Buy and Sell Stock IV (Code Studio)

Problem link : https://bit.ly/346R72e

## 1) Using Memoization 
- In this problem we can only buy and sell stock k times.
- when ind == n || cap ==0 return 0.
- When we buy, we have two options bay this stock or not. we return max of them.
- When we sell, we have two options sell this stock or not. we return max of them. Reduce the cap by one.

```C++
#include<bits/stdc++.h>
int fun(int ind,int buy,int cap,vector<int>& prices, int n,vector<vector<vector<int>>> &dp)
{
    if(ind == n || cap == 0) return 0;
    
    if(dp[ind][buy][cap] != -1) return dp[ind][buy][cap];
    
    if(buy == 1)
    {
        return dp[ind][buy][cap] = max(-prices[ind] + fun(ind+1,0,cap,prices,n,dp),
                   0 + fun(ind+1,1,cap,prices,n,dp));
    }
    else
    {
        return dp[ind][buy][cap] = max(prices[ind] + fun(ind+1,1,cap-1,prices,n,dp),
                   0 + fun(ind+1,0,cap,prices,n,dp));
    }
}
int maximumProfit(vector<int> &prices, int n, int k)
{
    vector<vector<vector<int>>> dp(n+1,vector<vector<int>>(2,vector<int>(k+1,-1)));
    
    return fun(0,1,k,prices,n,dp);
}
```

## 2) Using Tabulation

```C++
 int maximumProfit(vector<int> &prices, int n, int k)
{
    vector<vector<vector<int>>> dp(n+1,vector<vector<int>>(2,vector<int>(k+1,0)));
    
    for(int ind = n-1;ind>=0;ind--)
    {
        for(int buy=0; buy<=1;buy++)
        {
            for(int cap=1;cap<=k;cap++)
            {
                if(buy == 1)
                {
                    dp[ind][buy][cap] = max(-prices[ind] + dp[ind+1][0][cap],
                     0 + dp[ind+1][1][cap]);
                }
                else
                {
                    dp[ind][buy][cap] = max(prices[ind] + dp[ind+1][1][cap-1],
                    0 + dp[ind+1][0][cap]);
                }
            }
        }
    }
    return dp[0][1][k];
}

```

## 3) Using Space Optimization

```C++
int maximumProfit(vector<int> &prices, int n, int k)
{
    vector<vector<int>>after (2,vector<int>(k+1,0));
    vector<vector<int>>curr (2,vector<int>(k+1,0));
    
    for(int ind = n-1;ind>=0;ind--)
    {
        for(int buy=0; buy<=1;buy++)
        {
            for(int cap=1;cap<=k;cap++)
            {
                if(buy == 1)
                {
                    curr[buy][cap] = max(-prices[ind] + after[0][cap],
                     0 + after[1][cap]);
                }
                else
                {
                    curr[buy][cap] = max(prices[ind] + after[1][cap-1],
                    0 + after[0][cap]);
                }
            }
        }
        after = curr;
    }
    return after[1][k];
}

```
