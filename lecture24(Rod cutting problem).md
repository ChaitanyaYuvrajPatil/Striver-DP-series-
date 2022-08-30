# Leacture 24
Problem : Rod cutting problem (Code studio)

Problem link : https://bit.ly/3H10kYJ

## 1) Using Memoization
- In this problem we simply use take and not take method.
- In base case if we reach to index 0 we return N*price[0], because when we reach at end we cut rod in N pieces.
- Then we return and store max of take and not_take.

```C++
#include<bits/stdc++.h>
int fun(int ind,int N,vector<int> &price,vector<vector<int>> &dp)
{
    if(ind == 0)
    {
        return N*price[0];
    }
    
    if(dp[ind][N] != -1) return dp[ind][N];
    
    int not_take = fun(ind-1,N,price,dp);
    int take = INT_MIN;
    
    int rod_len = ind+1;
    if(rod_len <= N)
        take = price[ind] + fun(ind,N-rod_len,price,dp);
    
    return dp[ind][N] = max(take,not_take);
}

int cutRod(vector<int> &price, int n)
{
	vector<vector<int>> dp(n,vector<int>(n+1,-1));
    return fun(n-1,n,price,dp);
}
```

## 1) Using Tabulation

```C++
int cutRod(vector<int> &price, int n)
{
	vector<vector<int>> dp(n,vector<int>(n+1,0)); 
    for(int N=0;N<=n;N++)
    {
        dp[0][N] = N*price[0];
    }
    
    for(int ind = 1;ind<n; ind++)
    {
        for(int N = 0;N<=n; N++)
        {
             int not_take = dp[ind-1][N];  
             int take = INT_MIN;
    
             int rod_len = ind+1;
             if(rod_len <= N)
                take = price[ind] + dp[ind][N-rod_len];  
    
             dp[ind][N] = max(take,not_take);
        }
    }
    return dp[n-1][n];
}
```

## 1) Using Space Optimization

```C++
int cutRod(vector<int> &price, int n)
{
    vector<int> prev(n+1,0),curr(n+1,0);
    
    for(int N=0;N<=n;N++)
    {
        prev[N] = N*price[0];
    }
    
    for(int ind = 1;ind<n; ind++)
    {
        for(int N = 0;N<=n; N++)
        {
             int not_take = prev[N];  
             int take = INT_MIN;
    
             int rod_len = ind+1;
             if(rod_len <= N)
                take = price[ind] + curr[N-rod_len];  
    
             curr[N] = max(take,not_take);
        }
        prev = curr;
    }
    return prev[n];
}
```

