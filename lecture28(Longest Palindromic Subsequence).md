# Leacture 28
Problem : Longest Palindromic Subsequence (Code studio)

Problem link : https://www.codingninjas.com/codestudio/problems/longest-palindromic-subsequence_842787?leftPanelTab=0


## 1) Using Memoization
- This problem is same as finding longest subsequence.
- In this problem we pass two string in fun function which is s(provided) and another is reverse of s.


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

int longestPalindromeSubsequence(string s)
{
    string t = s;
    reverse(t.begin(),t.end());
    int n = s.size();
    
    vector<vector<int>> dp(n+1,vector<int>(n+1,-1));
    
    return fun(n,n,s,t,dp);
}
```


## 2) Using Tabulation

```C++
int longestPalindromeSubsequence(string s)
{
    string t = s;
    reverse(t.begin(),t.end());
    int n = s.size();
    
    vector<vector<int>> dp(n+1,vector<int>(n+1,0));
    
    for(int i=1;i<=n;i++)
    {
        for(int j=1;j<=n;j++)
        {
            if(s[i-1] == t[j-1]) 
                dp[i][j] = 1 + dp[i-1][j-1];  
            else
               dp[i][j] = 0 + max(dp[i-1][j],dp[i][j-1]);
        }
    }
    
    return dp[n][n];
}

```

## 3) Using Space Optimization

```C++
int longestPalindromeSubsequence(string s)
{
    string t = s;
    reverse(t.begin(),t.end());
    int n = s.size();
    
    vector<int>prev(n+1,0),curr(n+1,0);
    for(int i=1;i<=n;i++)
    {
        for(int j=1;j<=n;j++)
        {
            if(s[i-1] == t[j-1]) 
                curr[j] = 1 + prev[j-1];  
            else
               curr[j] = 0 + max(prev[j],curr[j-1]);
        }
        prev = curr;
    }
    return prev[n];
}
```

