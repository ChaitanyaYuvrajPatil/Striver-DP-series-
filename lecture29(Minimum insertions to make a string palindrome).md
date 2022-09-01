# Leacture 29
Problem : Minimum insertions to make a string palindrome (Code studio)

Problem link : https://bit.ly/3H2ZtGP


## 1) Using Memoization
- This problem is same as finding longest subsequence.
- In this problem we have to subtract length of longestPalindromeSubsequence from length of given string.

```C++
#include<bits/stdc++.h>
int fun(int i,int j,string s,string t,vector<vector<int>> &dp)
{
    if(i==0 || j==0) return 0;
    if(dp[i][j] != -1) return dp[i][j];
    
    if(s[i-1] == t[j-1])
        return dp[i][j] = 1 + fun(i-1,j-1,s,t,dp);
    return dp[i][j] = 0 + max(fun(i,j-1,s,t,dp),fun(i-1,j,s,t,dp));
}

int minInsertion(string &s)
{
    int n = s.size();
    string t = s;
    reverse(t.begin(),t.end());
    
    vector<vector<int>> dp(n+1,vector<int>(n+1,-1));
    return n - fun(n,n,s,t,dp);
}
```


## 2) Using Tabulation

```C++
int minInsertion(string &s)
{
    int n = s.size();
    string t = s;
    reverse(t.begin(),t.end());
    
    vector<vector<int>> dp(n+1,vector<int>(n+1,0));
    
    for(int i=1;i<=n;i++)
    {
        for(int j=1;j<=n;j++)
        {
            if(s[i-1] == t[j-1])
                dp[i][j] = 1 + dp[i-1][j-1];
            else 
                dp[i][j] = max(dp[i-1][j],dp[i][j-1]);
        }
    }
    return n - dp[n][n];
}
```

## 3) Using Space Optimization

```C++
int minInsertion(string &s)
{
    int n = s.size();
    string t = s;
    reverse(t.begin(),t.end());
    vector<int>prev(n+1,0),curr(n+1,0);
    
    for(int i=1;i<=n;i++)
    {
        for(int j=1;j<=n;j++)
        {
            if(s[i-1] == t[j-1])
                curr[j] = 1 + prev[j-1];
            else 
                curr[j] = max(prev[j],curr[j-1]);
        }
        prev = curr;
    }
    return n - prev[n];
}
```

