# Leacture 51
Problem : Mining Diamonds (Code Studio)

Problem link : https://bit.ly/3Kgck9N

## 1) Using Memoization 

- In this problem we first insert 1 at begin and 1 at end in cuts array.
- In fun() function we are checking every posibility for cuts from i to j.
- In base case if i>j return 0.
- Peacked the minimum and return and store it in dp.

```C++
#include<bits/stdc++.h>

int fun(int i,int j,vector<int>& a,vector<vector<int>> &dp)
{
    if(i>j) return 0;
    
    if(dp[i][j] != -1) return dp[i][j];
    
    int mx = -1e9;
    
    for(int k=i;k<=j;k++)
    {
        int coin = a[i-1]*a[k]*a[j+1] + fun(i,k-1,a,dp) + fun(k+1,j,a,dp);
        mx = max(mx,coin);
    }
    return dp[i][j] = mx;
}
int maxCoins(vector<int>& a)
{
    
	int n = a.size();
    a.insert(a.begin(),1);
    a.push_back(1);
    
    vector<vector<int>> dp(n+1,vector<int>(n+1,-1));
    return fun(1,n,a,dp);   
}
```

## 2) Using Tabulation

```C++
 #include<bits/stdc++.h>
 int maxCoins(vector<int>& a)
{
    
	int n = a.size();
    a.insert(a.begin(),1);
    a.push_back(1);
    
    vector<vector<int>> dp(n+2,vector<int>(n+2,0));
    
    for(int i=n;i>=1;i--)
    {
        for(int j=1;j<=n;j++)
        {
            if(i>j) continue;
            
            int mx = -1e9;
            for(int k=i;k<=j;k++)
            {
                int coin = a[i-1]*a[k]*a[j+1] + dp[i][k-1] + dp[k+1][j];
                mx = max(mx,coin);
            }
            dp[i][j] = mx;
        }
    }
    return dp[1][n];   
}
```
