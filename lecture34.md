# Leacture 34
Problem : Wildcard Matching (Code Studio)

Problem link : https://bit.ly/3qXtORt

## 1) Using Memoization 
- In base case there are three conditions 1) if(i<0 && j<0) We are returning true (both string are exuasted).
  2) if(i<0 && j>=0) return false (pattern string is exausted).
  3) if(i>=0 && j<0) means text string is exausted. we are checking that every character in pattern string is * or not up to i, if * we return true,if not we return false.
- if(pattern[i] == text[j] || pattern[i] == '?') we simply move back by one in both string.
- if(pattern[i] == '*') we return or of fun(i-1,j,pattern,text,dp) (selecting no character in text string), fun(i,j-1,pattern,text,dp);
- else return false.

```C++
#include<bits/stdc++.h>
bool fun(int i,int j,string pattern, string text,vector<vector<int>> &dp)
{
    if(i<0 && j<0) return true;
    if(i<0 && j>=0) return false;
    if(i>=0 && j<0)
    {
        for(int k=0;k<=i;k++)
        {
            if(pattern[k] != '*') return false;
        }
        return true;
    }
    
    if(dp[i][j] != -1) return dp[i][j];
    
    if(pattern[i] == text[j] || pattern[i] == '?')
        return dp[i][j] =  fun(i-1,j-1,pattern,text,dp);
    
    if(pattern[i] == '*')
    {
        return dp[i][j] = fun(i-1,j,pattern,text,dp) | fun(i,j-1,pattern,text,dp);
    }
    
    return dp[i][j] = false;
}
bool wildcardMatching(string pattern, string text)
{
    int n = pattern.size();
    int m = text.size();  
    vector<vector<int>> dp(n+1,vector<int>(m+1,-1));
        
    return fun(n-1,m-1,pattern,text,dp);
}

```
### Or (Using one base indexing)
```C++
#include<bits/stdc++.h>
bool fun(int i,int j,string pattern, string text,vector<vector<int>> &dp)
{
    if(i==0 && j==0) return true;
    if(i==0 && j>0) return false;
    if(i>0 && j==0)
    {
        for(int k=1;k<=i;k++)
        {
            if(pattern[k-1] != '*') return false;
        }
        return true;
    }
    
    if(dp[i][j] != -1) return dp[i][j];
    
    if(pattern[i-1] == text[j-1] || pattern[i-1] == '?')
        return dp[i][j] =  fun(i-1,j-1,pattern,text,dp);
    
    if(pattern[i-1] == '*')
    {
        return dp[i][j] = fun(i-1,j,pattern,text,dp) | fun(i,j-1,pattern,text,dp);
    }
    
    return dp[i][j] = false;
}
bool wildcardMatching(string pattern, string text)
{
    int n = pattern.size();
    int m = text.size();
    
    vector<vector<int>> dp(n+1,vector<int>(m+1,-1));
    return fun(n,m,pattern,text,dp);
}

```

## 2) Using Tabulation

```C++
bool wildcardMatching(string pattern, string text)
{
    int n = pattern.size();
    int m = text.size();
    
    vector<vector<bool>> dp(n+1,vector<bool>(m+1,false));
    
    dp[0][0] = true;
    for(int j=1;j<=m;j++)
    {
        dp[0][j] = false;
    }
    
    for(int i=1;i<=n;i++)
    {
        bool flag = true;
        for(int k=1;k<=i;k++)
        {
            if(pattern[k-1] != '*')
            {
                flag = false;
                break;
            }
        }
        dp[i][0] = flag;
    }
    
    for(int i=1;i<=n;i++)
    {
        for(int j=1;j<=m;j++)
        {
            if(pattern[i-1] == text[j-1] || pattern[i-1] == '?')
            {
                dp[i][j] = dp[i-1][j-1]; 
            }
            else if(pattern[i-1] == '*')
            {
                dp[i][j] = dp[i-1][j] | dp[i][j-1]; 
            }
            else dp[i][j] = false;
        }
    }
    
   return dp[n][m];
}

```

## 3) Using Space Optimization

```C++
bool wildcardMatching(string pattern, string text)
{
    int n = pattern.size();
    int m = text.size();
    
    vector<bool>prev(m+1,false),curr(m+1,false);
    prev[0] = true;
    for(int i=1;i<=n;i++)
    {
        bool flag = true;
        for(int k=1;k<=i;k++)
        {
            if(pattern[k-1] != '*')
            {
                flag = false;
                break;
            }
        }
        curr[0] = flag;
        
        for(int j=1;j<=m;j++)
        {
            if(pattern[i-1] == text[j-1] || pattern[i-1] == '?')
            {
                curr[j] = prev[j-1]; 
            }
            else if(pattern[i-1] == '*')
            {
                curr[j] = prev[j] | curr[j-1]; 
            }
            else curr[j] = false;
        }
        prev = curr;
    }  
   return prev[m];
}

```
