# Leacture 39
Problem : Best Time to Buy and Sell Stock with Cooldown (Code Studio)

Problem link : https://bit.ly/3tZsYWA

## 1) Using Memoization 
- This Problem is similar as previous one.
- In this we can not buy emidiately stock after selling it. We can buy after one cell.

```C++
#include<bits/stdc++.h>
int fun(int ind,int buy,vector<int> &prices, vector<vector<int>> &dp)
{
    if(ind >= prices.size())
        return 0;
    
    if(dp[ind][buy] != -1) return dp[ind][buy];
    
    if(buy == 1)
    {
        return dp[ind][buy] =  max(-prices[ind] + fun(ind+1,0,prices,dp),
                                   0 + fun(ind+1,1,prices,dp));
    }
    else
    {
        return  dp[ind][buy] =  max(prices[ind] + fun(ind+2,1,prices,dp),
                                     0 + fun(ind+1,0,prices,dp));
    }
}

int stockProfit(vector<int> &prices){
    int n = prices.size();
    vector<vector<int>> dp(n+2,vector<int>(2,-1));
   
    return fun(0,1,prices,dp);
}
```

## 2) Using Tabulation

```C++
 int stockProfit(vector<int> &prices){
    int n = prices.size();
    
    vector<vector<int>> dp(n+2,vector<int>(2,0));
    
    for(int ind = n-1;ind>=0; ind--)
    {
        for(int buy = 0;buy<=1;buy++)
        {
            if(buy == 1)
            {
               dp[ind][buy] =  max(-prices[ind] + dp[ind+1][0], 0 + dp[ind+1][1]);
            }
            else
            {
               dp[ind][buy] =  max(prices[ind] + dp[ind+2][1],
                                     0 + dp[ind+1][0]);
            }
        }
    }
    
    return dp[0][1];
}
```

## 3) Using Space Optimization

```C++
int stockProfit(vector<int> &prices){
    int n = prices.size();
    vector<int>front2(2,0);
    vector<int>front1(2,0);
    vector<int>curr(2,0);
    
    for(int ind = n-1;ind>=0; ind--)
    {
        for(int buy = 0;buy<=1;buy++)
        {
            if(buy == 1)
            {
               curr[buy] =  max(-prices[ind] + front1[0], 0 + front1[1]);
            }
            else
            {
               curr[buy] =  max(prices[ind] + front2[1],
                                     0 + front1[0]);
            }
        }
        front2 = front1;
        front1 = curr;
    } 
    return curr[1];
}

```
