# Leacture 25
Problem : Longest Common Subsequence (Code studio)

Problem link : https://bit.ly/3pvkqUd

## 1) Using Memoization
- In this problem we are checking posibilities.(traversing from back).
- We only include when letters of string are matching.
- If they are not matching then we check every posibility, one time we decrease ind1 by 1 and ind2 be stedy, another time vice versa.
- In base case we if ind1 or ind2 becomes less than 0 return 0.

```C++
#include<bits/stdc++.h>
int fun(int ind1,int ind2,string s, string t,vector<vector<int>> &dp)
{
    if(ind1<0 || ind2<0) return 0;
    
    if(dp[ind1][ind2] != -1) return dp[ind1][ind2];
    
    if(s[ind1] == t[ind2]) 
        return dp[ind1][ind2] = 1 + fun(ind1-1,ind2-1,s,t,dp);
    
    return dp[ind1][ind2] = 0 + max(fun(ind1-1,ind2,s,t,dp),fun(ind1,ind2-1,s,t,dp));
}
int lcs(string s, string t)
{
	int m = s.size();
    int n = t.size();
    vector<vector<int>> dp(m,vector<int>(n,-1));
    
    return fun(m-1,n-1,s,t,dp);
}
```
###   Or (Using shifting index in Memoization)

```C++
#include<bits/stdc++.h>
int fun(int ind1,int ind2,string s, string t,vector<vector<int>> &dp)
{
    if(ind1 == 0 || ind2 == 0) return 0;
    
    if(dp[ind1][ind2] != -1) return dp[ind1][ind2];
    
    if(s[ind1-1] == t[ind2-1]) 
        return dp[ind1][ind2] = 1 + fun(ind1-1,ind2-1,s,t,dp);
    
    return dp[ind1][ind2] = 0 + max(fun(ind1-1,ind2,s,t,dp),fun(ind1,ind2-1,s,t,dp));
}
int lcs(string s, string t)
{
	int m = s.size();
    int n = t.size();
    
    vector<vector<int>> dp(m+1,vector<int>(n+1,-1));
    
    return fun(m,n,s,t,dp);
}

```

## 2) Using Tabulation
- In this method we traversing from bottom to top.
- In this solution we are shifting base indexes by 1, for base case to satisfy.
```C++
int lcs(string s, string t)
{
	int m = s.size();
    int n = t.size();
    vector<vector<int>> dp(m+1,vector<int>(n+1,0));
    
    for(int i=0;i<=m;i++) dp[i][0] = 0;
    for(int j=0;j<=n;j++) dp[0][j] = 0;
    
    for(int i=1; i<=m; i++)
    {
        for(int j=1; j<=n; j++)
        {
            if(s[i-1] == t[j-1]) 
                dp[i][j] = 1 +  dp[i-1][j-1]; 
            else
                dp[i][j] = 0 + max(dp[i-1][j],dp[i][j-1]);
        }
    }
    return  dp[m][n]; 
}

```

## 3) Using Space Optimization
- We are using two prev and curr array for storing previous and current position.
```C++
int lcs(string s, string t)
{
	int m = s.size();
    int n = t.size();
    vector<int> prev(n+1,0),curr(n+1,0);
    
    for(int j=0;j<=n;j++) prev[j] = 0;
    
    for(int i=1; i<=m; i++)
    {
        for(int j=1; j<=n; j++)
        {
            if(s[i-1] == t[j-1]) 
                curr[j] = 1 +  prev[j-1]; 
            else
                curr[j] = 0 + max(prev[j],curr[j-1]);
        }
        prev = curr;
    }
    return  prev[n]; 
}
```

