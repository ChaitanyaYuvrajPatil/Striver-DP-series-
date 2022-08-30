# Leacture 22
Problem : Ways To Make Coin Change/Coin Change 2 (Code studio)

Problem link : https://bit.ly/33Kd8o2

## 1) Using Memoization
- In this problem we simply use take and not take method.
- In base case if we reach to index 0 we return 1 if val is divisible by a[0].
- In take condition if val >= a[ind] then we change val and move to the same index.(we allow to take same coin multiple times).
- Then we return and store take + not_take.

```C++
#include<bits/stdc++.h>
long fun(int ind,int val,int *a,vector<vector<long>> &dp )
{
    if(ind == 0)
    {
        if(val % a[0] == 0) return 1;
        else return 0;
    }
    
    if(dp[ind][val] != -1) return dp[ind][val];
    long not_take = fun(ind-1,val,a,dp);
    long take = 0;
    
    if(val >= a[ind])
        take = fun(ind,val-a[ind],a,dp);
    
    dp[ind][val] = take+not_take;
}

long countWaysToMakeChange(int *denominations, int n, int value)
{
    vector<vector<long>> dp(n,vector<long>(value+1,-1));
    return fun(n-1,value,denominations,dp);
}
```

## 1) Using Tabulation

```C++
#include<bits/stdc++.h>
long countWaysToMakeChange(int *a, int n, int value)
{
    vector<vector<long>> dp(n,vector<long>(value+1,0));
    
    for(int val = 0;val<=value; val++)
    {
        dp[0][val] = (val % a[0] == 0);
    }
    
    for(int ind =1;ind < n;ind++)
    {
        for(int val = 0; val<= value; val++)
        {
            long not_take = dp[ind-1][val];
            long take = 0;
    
            if(val >= a[ind])
               take = dp[ind][val-a[ind]];
    
            dp[ind][val] = take+not_take;
        }
    }
    return dp[n-1][value];
}
```

## 1) Using Space Optimization

```C++
long countWaysToMakeChange(int *a, int n, int value)
{
    vector<long> prev(value+1,0),curr(value+1,0);
    
    for(int val = 0;val<=value; val++)
    {
        prev[val] = (val % a[0] == 0);
    }
    
    for(int ind =1;ind < n;ind++)
    {
        for(int val = 0; val<= value; val++)
        {
            long not_take = prev[val];
            long take = 0;
    
            if(val >= a[ind])
               take = curr[val-a[ind]];
    
            curr[val] = take+not_take;
        }
        prev = curr;
    }
    return prev[value];
}
```

