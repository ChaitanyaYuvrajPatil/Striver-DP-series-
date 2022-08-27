# Leacture 11

Problem : Triangle (Code studio)

Problem link : https://bit.ly/3K1cvqv

## 1) Using Memoization
- In problem we traverse from back.
- base case will execute when it reach to last row which is if(i==n-1) return tri[i][j].
- then we calculate down and diagonal.
- Return and store minimum of down and diagonal.

```C++
int fun(int i,int j,int n,vector<vector<int>>& tri,vector<vector<int>> &dp)
{
    if(i==n-1) return tri[i][j];
    if(dp[i][j] != -1) return dp[i][j];
    
    int down = tri[i][j] + fun(i+1,j,n,tri,dp);
    int diag = tri[i][j] + fun(i+1,j+1,n,tri,dp);
    
    return dp[i][j] = min(down,diag);
}

int minimumPathSum(vector<vector<int>>& tri, int n){
    
    vector<vector<int>> dp(n,vector<int>(n,-1));
    
    return fun(0,0,n,tri,dp);
}
```

## 1) Using Tabulation
- First we declare dp array of size nxn.
- First we store last row of tri in last row of dp.
- We start traversing from i=n-2 to 0. In nested j=i to 0.
- Then we calculate down and diagonal.
- Return and store minimum of down and diagonal.
- Return dp[0][0].

```C++
int minimumPathSum(vector<vector<int>>& tri, int n){
    
    vector<vector<int>> dp(n,vector<int>(n,-1));
    
    for(int i=n-1;i>=0;i--)
    {
        dp[n-1][i] = tri[n-1][i];
    }
    
    for(int i=n-2;i>=0; i--)
    {     
        for(int j=i;j>=0; j--)
        {
            int d = tri[i][j] + dp[i+1][j];
            int dia = tri[i][j] + dp[i+1][j+1];       
            dp[i][j] = min(d,dia);
        }
    }
    return dp[0][0];
}
```

## 1) Space Optimization
- In this solution we simply make prev and curr array.
- As we need only need down and diagonal  value.

```C++
int minimumPathSum(vector<vector<int>>& tri, int n){
    vector<int>prev(n,-1);
    for(int i=n-1;i>=0;i--)
    {
        prev[i] = tri[n-1][i];
    }
    
    for(int i=n-2;i>=0; i--)
    {     
        vector<int>curr(n,-1);
        for(int j=i;j>=0; j--)
        {
            int d = tri[i][j] + prev[j];
            int dia = tri[i][j] + prev[j+1];       
            curr[j] = min(d,dia);
        }
        prev = curr;
    }
    return prev[0];
}
```

