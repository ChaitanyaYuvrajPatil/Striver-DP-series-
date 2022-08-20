# Leacture 48
Problem : Matrix Chain Multiplication (Code Studio)

Problem link : https://bit.ly/3nXqfce

## 1) Using Memoization 

```C++
#include<bits/stdc++.h>
int fun(int i,int j,vector<int> &arr,vector<vector<int>> &dp)
{
    if(i==j) return 0;
    int mn = 1e9;
    
    if(dp[i][j] != -1) return dp[i][j];
  
    for(int k=i;k<j;k++)
    {
        int step = arr[i-1]*arr[k]*arr[j] + fun(i,k,arr,dp) + fun(k+1,j,arr,dp);
        mn = min(mn,step);
    }
    return dp[i][j] =  mn;
}
int matrixMultiplication(vector<int> &arr, int N)
{
    vector<vector<int>> dp(N,vector<int>(N,-1));
    return fun(1,N-1,arr,dp);
}

```

## 2) Using Tabulation

```C++
 int matrixMultiplication(vector<int> &arr, int N)
{
    vector<vector<int>> dp(N,vector<int>(N,0));
    
    for(int i=N-1;i>=1;i--)
    {
        for(int j = i+1;j<N;j++)
        {
            int mn = 1e9;
            for(int k=i;k<j;k++)
            {
                 int step = arr[i-1]*arr[k]*arr[j] + dp[i][k] + dp[k+1][j];
                 mn = min(mn,step);
            }
            dp[i][j] =  mn;
        }
    } 
    return dp[1][N-1];
}
```
