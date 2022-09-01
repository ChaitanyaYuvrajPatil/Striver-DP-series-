# Leacture 30
Problem : Minimum Number of Deletions and Insertions (Code studio)

Problem link : https://bit.ly/3pya8CP

## 1) Using Memoization
- This problem is same as finding longest subsequence.
- Number of delition equal to (length of first string) - lcs.
- Number of insertion equal to (length of second string) - lcs.
- Answer will be sum of Numberof insertion and delition.

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

int canYouMake(string &s, string &t)
{
    int n = s.size();
    int m = t.size();
    vector<vector<int>> dp(n+1,vector<int>(m+1,-1));
    return n + m - 2*fun(n,m,s,t,dp);
}
```


## 2) Using Tabulation

```C++
int canYouMake(string &s, string &t)
{
    int n = s.size();
    int m = t.size();
    vector<vector<int>> dp(n+1,vector<int>(m+1,0));
    
    for(int i=1;i<=n;i++)
    {
        for(int j=1;j<=m;j++)
        {
            if(s[i-1] == t[j-1])
                dp[i][j] = 1 + dp[i-1][j-1];
            else 
                dp[i][j] = max(dp[i-1][j],dp[i][j-1]);
        }
    }
    return n+m - 2*dp[n][m];
}
```

## 3) Using Space Optimization

```C++
int canYouMake(string &s, string &t)
{
    int n = s.size();
    int m = t.size();
    vector<int>prev(m+1,0),curr(m+1,0);
    
    for(int i=1;i<=n;i++)
    {
        for(int j=1;j<=m;j++)
        {
            if(s[i-1] == t[j-1])
                curr[j] = 1 + prev[j-1];
            else 
                curr[j] = max(prev[j],curr[j-1]);
        }
        prev = curr;
    }
    return n+m - 2*prev[m];
}
```

