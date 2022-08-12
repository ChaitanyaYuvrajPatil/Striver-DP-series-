# Leacture 30
Problem : Distinct Subsequences (leetcode)

Problem link : https://leetcode.com/problems/distinct-subsequences/

## 1) Using Memoization (Gives TLE)
- In this Problem we finding number of occurances of string t in s.
- In base case we return 1 only when j is less than 0. It means string found else we return 0.
- When s[i] matches with  t[j] we check two posibilities and add them.
- In first if both matches we dicrease both indexes by one.
- In second we decrese only first index.
- In else part we decrese only first index, as no string matches.

```C++
class Solution {
public:
    
    int fun(int i,int j,string s, string t,vector<vector<int>> &dp)
    {
        if(j<0) return 1;
        if(i<0) return 0;
        
        if(dp[i][j] != -1) return dp[i][j];
        
        if(s[i] == t[j])
            return dp[i][j] =  fun(i-1,j-1,s,t,dp) + fun(i-1,j,s,t,dp);
        else
            return dp[i][j] = fun(i-1,j,s,t,dp);
    }
    
    int numDistinct(string s, string t) {
        
        int n = s.size();
        int m = t.size();
        
        vector<vector<int>> dp(n,vector<int>(m,-1));
        
        return fun(n-1,m-1,s,t,dp);
    }
};
```
### Or (Using one base indexing)
```C++
class Solution {
public:
    
    int fun(int i,int j,string s, string t,vector<vector<int>> &dp)
    {
        if(j==0) return 1;
        if(i==0) return 0;
        
        if(dp[i][j] != -1) return dp[i][j];
        
        if(s[i-1] == t[j-1])
            return dp[i][j] =  fun(i-1,j-1,s,t,dp) + fun(i-1,j,s,t,dp);
        else
            return dp[i][j] = fun(i-1,j,s,t,dp);
    }
    
    int numDistinct(string s, string t) {
        
        int n = s.size();
        int m = t.size();
        
        vector<vector<int>> dp(n+1,vector<int>(m+1,-1));
        
        return fun(n,m,s,t,dp);
    }
};
```

## 2) Using Tabulation

```C++
int numDistinct(string s, string t) {
        
        int n = s.size();
        int m = t.size();
        
        vector<vector<double>> dp(n+1,vector<double>(m+1,0));
        
        for(int i=0;i<=n;i++) dp[i][0] = 1;
        
        
        for(int i=1;i<=n;i++)
        {
            for(int j=1;j<=m;j++)
            {
                if(s[i-1] == t[j-1])
                    dp[i][j] = dp[i-1][j-1] + dp[i-1][j]; 
                else
                    dp[i][j] = dp[i-1][j]; 
            }
        }
        
        return (int)dp[n][m]; 
}
```

## 3) Using Space Optimization

```C++
int numDistinct(string s, string t) {
        
        int n = s.size();
        int m = t.size();
        
        vector<double> prev(m+1,0),curr(m+1,0);
        
        prev[0] = curr[0] = 1;
        
        for(int i=1;i<=n;i++)
        {
            for(int j=1;j<=m;j++)
            {
                if(s[i-1] == t[j-1])
                    curr[j] = prev[j-1] + prev[j]; 
                else
                    curr[j] = prev[j]; 
            }
            prev = curr;
        }
        
        return (int)prev[m]; 
}
```

## 4) 1-D Optimization

```C++
int numDistinct(string s, string t) {
        
        int n = s.size();
        int m = t.size();
        
        vector<double> prev(m+1,0);
        
        prev[0] = 1;
        
        for(int i=1;i<=n;i++)
        {
            for(int j=m;j>=1;j--) // From m to 1
            {
                if(s[i-1] == t[j-1])
                    prev[j] = prev[j-1] + prev[j]; 
            }
        }
        
        return (int)prev[m]; 
    }
```



