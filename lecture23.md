# Leacture 23
Problem : Unbounded Knapsack (Code studio)

Problem link : https://bit.ly/3IvPdXS

## 1) Using Memoization
- In this problem we simply use take and not take method.
- In base case if we reach to index 0 we return (w/weight[0])*profit[0], because when at end we can pick up w/weight[0] items of weight weight[0].
- In take condition if weight[ind] <= w then we change val and move to the same index.(we allow to take same weight multiple times).
- Then we return and store take + not_take.

```C++
#include<bits/stdc++.h>
int fun(int ind,int w, vector<int> &profit, vector<int> &weight,vector<vector<int>> &dp)
{
    if(ind == 0)
    {
        return (w/weight[0])*profit[0];
    }
    
    if(dp[ind][w] != -1) return dp[ind][w];
    int not_take = fun(ind-1,w,profit,weight,dp);
    int take = INT_MIN;
    
    if(weight[ind] <= w)
        take = profit[ind] + fun(ind,w-weight[ind],profit,weight,dp);
    
    dp[ind][w] = max(take,not_take);
}

int unboundedKnapsack(int n, int w, vector<int> &profit, vector<int> &weight)
{
    vector<vector<int>> dp(n,vector<int>(w+1,-1));
    
    return fun(n-1,w,profit,weight,dp);   
}
```

## 1) Using Tabulation

```C++
int unboundedKnapsack(int n, int w, vector<int> &profit, vector<int> &weight)
{
    vector<vector<int>> dp(n,vector<int>(w+1,0));
    
    for(int wt = 0; wt<= w; wt++)
    {
        dp[0][wt] = ((int)(wt/weight[0]))*profit[0];
    }
    
    for(int ind = 1;ind<n; ind++)
    {
        for(int wt = 0; wt<=w; wt++)
        {
            int not_take = 0 + dp[ind-1][wt]; 
            int take = 0;
    
            if(weight[ind] <= wt)
               take = profit[ind] + dp[ind][wt-weight[ind]]; 
    
            dp[ind][wt] = max(take,not_take);
        }
    }
    return dp[n-1][w];
}

```

## 1) Using Space Optimization

```C++
int unboundedKnapsack(int n, int w, vector<int> &profit, vector<int> &weight)
{
    vector<vector<int>> dp(n,vector<int>(w+1,0));
    vector<int> prev(w+1,0),curr(w+1,0);
    
    for(int wt = 0; wt<= w; wt++)
    {
        prev[wt] = ((int)(wt/weight[0]))*profit[0];
    }
    
    for(int ind = 1;ind<n; ind++)
    {
        for(int wt = 0; wt<=w; wt++)
        {
            int not_take = 0 + prev[wt]; 
            int take = 0;
    
            if(weight[ind] <= wt)
               take = profit[ind] + curr[wt-weight[ind]]; 
    
            curr[wt] = max(take,not_take);
        }
        prev = curr;
    }
    return prev[w];
}
```

