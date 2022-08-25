# Leacture 8

Problem : Unique Paths (Code studio)

Problem link : https://bit.ly/34uoYCG

## 1) Using Memoization
- In this problem we create 2D dp array of size mxn.
- Writing base case from i=0 and i=j where value id 1 (no of path).Also if we get negative index return 0.
- then sum up left and up and store in dp[i][j].

```C++
#include <bits/stdc++.h> 
int fun(int i,int j,vector<vector<int>>&dp)
{
    if(i == 0 && j == 0)
        return 1;
    
    if(i<0 || j<0) return 0;
    
    if(dp[i][j] != 0) return dp[i][j];
    
    int up = fun(i-1,j,dp);
    int left = fun(i,j-1,dp);
    
    return dp[i][j] = up+left;
}
int uniquePaths(int m, int n) {
    vector<vector<int>>dp(m,vector<int>(n,0));
    return fun(m-1,n-1,dp);
}
```

## 1) Using Tabulation
- In this problem we create 2D dp array of size mxn.
- We traverse from [0][0] to [m-1][n-1].

```C++

int uniquePaths(int m, int n) {
    vector<vector<int>>dp(m,vector<int>(n));
    //dp[0][0] = 1;
    for(int i=0;i<m;i++)
    {
        for(int j=0;j<n;j++)
        {
            if(i==0 && j==0) dp[i][j] = 1;
            else
            {
              int up = 0, left =0;
              if(i > 0)
                 up = dp[i-1][j];
              if(j > 0)
                 left = dp[i][j-1];
            
              dp[i][j] = up+left;
            }
        }
    }
    return dp[m-1][n-1];
}
```

## 1) Space Optimization
- In this solution we store only previous row and current row.
- After we process current row(temp). we make it as previous.


```C++
int uniquePaths(int m, int n) {
    vector<int>prev(n,0);
    for(int i=0;i<m;i++)
    {
        vector<int>temp(n,0);
        for(int j=0;j<n;j++)
        {
            if(i==0 && j==0) temp[j] = 1;
            else
            {
              int up = 0, left =0;
              if(i > 0)
                 up = prev[j];
              if(j > 0)
                 left = temp[j-1];
            
              temp[j] = up+left;
            }
        }
        prev = temp;
    }
    return prev[n-1];
}
```

