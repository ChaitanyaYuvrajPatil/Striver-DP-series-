# Leacture 41
Problem : Longest Increasing Subsequence (Code Studio)

Problem link : https://bit.ly/3rVoIoq

## 1) Using Memoization 
- Simple take or not take approch.

```C++
#include<bits/stdc++.h>
int fun(int ind,int prev,int arr[], int n,vector<vector<long>> &dp)
{
    if(ind == n) return 0;
    
    if(dp[ind][prev+1] != -1) return dp[ind][prev+1];
    int len = fun(ind+1,prev,arr,n,dp);
    
    if(prev == -1 || arr[prev] < arr[ind])
    {
        len = max(len, 1 + fun(ind+1,ind,arr,n,dp));
    }
    
    return dp[ind][prev+1] = len;
}
int longestIncreasingSubsequence(int arr[], int n)
{
    vector<vector<long>> dp(n,vector<long>(n+1,-1));
    
    return fun(0,-1,arr,n,dp);
}

```

## 2) Using Tabulation

```C++
 int longestIncreasingSubsequence(int arr[], int n)
{
    vector<vector<long>> dp(n+1,vector<long>(n+1,0));
    
    for(int ind = n-1;ind>=0;ind--)
    {
        for(int prev = ind-1;prev>=-1;prev--)
        {
            int len = 0 + dp[ind+1][prev+1]; 
    
            if(prev == -1 || arr[prev] < arr[ind])
            {
                if(1 + dp[ind+1][ind+1] > len)
                    len = 1 + dp[ind+1][ind+1];
            }
            dp[ind][prev+1] = len;
        }
    }
    return dp[0][0];
}

```

## 3) Using Space Optimization

```C++
int longestIncreasingSubsequence(int arr[], int n)
{
    vector<long>next(n+1,0),curr(n+1,0);
    
    for(int ind = n-1;ind>=0;ind--)
    {
        for(int prev = ind-1;prev>=-1;prev--)
        {
            int len = 0 + next[prev+1]; 
    
            if(prev == -1 || arr[prev] < arr[ind])
            {
                if(1 + next[ind+1] > len)
                    len = 1 + next[ind+1];
            }
            curr[prev+1] = len;
        }
        next = curr;
    }
    return next[0];
}

```
### Or (1 D space)
- First We store 1 in dp array of size 1.
- In loops update dp[ind] = max(dp[ind],1 + dp[prev]) when arr[ind] > arr[prev].
- Take max mx = max(mx,dp[ind]).
- Return max.

```C++
int longestIncreasingSubsequence(int arr[], int n)
{
    vector<int>dp(n,1);
    int mx = 1;
    for(int ind=0;ind<n;ind++)
    {
        for(int prev=0;prev<ind;prev++)
        {
            if(arr[ind] > arr[prev])
                dp[ind] = max(dp[ind],1 + dp[prev]);
        }
        mx = max(mx,dp[ind]);
    }  
    return mx;
}
```
