# Leacture 9

Problem : Unique Paths II (Code studio)

Problem link : https://bit.ly/3JMHc2l

## 1) Using Memoization
- All logic is same as previous problem.(Leacture 8)
- We adding just one condition if mat[i][j] == -1 then return 0.

```C++
int mod = (int)(1e9 +7);

int fun(int i, int j,vector< vector< int> > &mat,vector<vector<int>>&dp)
{
    if(i>=0 && j>=0 && mat[i][j] == -1) return 0;
    if(i<0 || j<0) return 0;
    if(i==0 && j==0) return 1;
    
    if(dp[i][j] != -1) return dp[i][j];
    
    int up = fun(i-1,j,mat,dp);
    int left = fun(i,j-1,mat,dp);
    
    return dp[i][j] = (up+left)%mod;
}

int mazeObstacles(int n, int m, vector< vector< int> > &mat) {
    vector<vector<int>>dp(n,vector<int>(m,-1));
    return fun(n-1,m-1,mat,dp);
}
```

## 1) Using Tabulation
- All logic is same as previous problem.(Leacture 8)
- We adding just one condition if mat[i][j] == -1 then dp[i][j] = 0.

```C++
int mazeObstacles(int n, int m, vector< vector< int> > &mat) {
    int mod = (int)(1e9 +7);
    vector<vector<int>>dp(n,vector<int>(m,0));
    
    for(int i=0;i<n;i++)
    {
        for(int j=0;j<m;j++)
        {
            if(mat[i][j] == -1) dp[i][j] = 0;
            else if(i ==0 && j==0) dp[i][j] = 1;
            else{
                int left=0,up=0;
                if(i>0)
                    up = dp[i-1][j];
                if(j>0)
                    left = dp[i][j-1];
                
                dp[i][j] = (up+left)%mod;
            }
        }
    }
    
    return dp[n-1][m-1];
}
```

## 1) Space Optimization
- All logic is same as previous problem.(Leacture 8)
- We adding just one condition if mat[i][j] == -1 then temp[j] = 0.

```C++
int mazeObstacles(int n, int m, vector< vector< int> > &mat) {
    int mod = (int)(1e9 +7);
    vector<int>prev(n,0);
    for(int i=0;i<n;i++)
    {
        vector<int>temp(m,0);
        for(int j=0;j<m;j++)
        {
            if(mat[i][j] == -1) temp[j] = 0;
            else if(i ==0 && j==0) temp[j] = 1;
            else{
                int left=0,up=0;
                if(i>0)
                    up = prev[j];
                if(j>0)
                    left = temp[j-1];
                
                temp[j] = (up+left)%mod;
            }
        }
        prev = temp;
    }
    
    return prev[m-1];
}
```

