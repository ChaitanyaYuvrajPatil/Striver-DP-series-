# Leacture 12

Problem : Maximum Path Sum in the matrix (Code studio)

Problem link : https://bit.ly/3F436dK

## 1) Using Memoization
- First we declare dp array of size nxm.
- In problem we traverse from back.
- base case will execute when it reach to last row which is if(j>=mat[0].size() || j<0) return -1e9.
- then we calculate left,mid and right.
- Return and store miximum of left,mid and right.

```C++
int fun(int i,int j,vector<vector<int>> &mat,vector<vector<int>> &dp)
{
    if(j>=mat[0].size() || j<0) return -1e9;
    
    if(i==0) return mat[i][j];
    
    if(dp[i][j] != -1) return dp[i][j];
    
    int left = mat[i][j] + fun(i-1,j-1,mat,dp);
    int mid = mat[i][j] + fun(i-1,j,mat,dp);
    int right = mat[i][j] + fun(i-1,j+1,mat,dp);
    
    return dp[i][j] =  max(left,max(mid,right));
}
int getMaxPathSum(vector<vector<int>> &mat)
{
    int n = mat.size();
    int m = mat[0].size();
    vector<vector<int>> dp(n,vector<int>(m,-1));
    int mx = -1e9;
    for(int i=0;i<m;i++)
    {
        mx = max(mx,fun(n-1,i,mat,dp));
    }  
    return mx;
}
```

## 1) Using Tabulation
- First we declare dp array of size nxm.
- First we store first row of mat in first row of dp.
- We start traversing from i=1 to n. In nested j=0 to m.
- then we calculate left,mid and right.
- Return and store miximum of left,mid and right.
- Then we return maximum of last row of dp matrix

```C++
int getMaxPathSum(vector<vector<int>> &mat)
{
    int n = mat.size();
    int m = mat[0].size();
    vector<vector<int>> dp(n,vector<int>(m,-1));
    for(int i=0;i<m;i++)
    {
        dp[0][i] = mat[0][i];
    }
    
    for(int i=1;i<n;i++)
    {
        for(int j=0;j<m;j++)
        {
            int left = -1e9,right = -1e9;
            if(j>0)
               left = mat[i][j] + dp[i-1][j-1];
            int mid = mat[i][j] + dp[i-1][j];
            if(j+1 < m)
               right = mat[i][j] + dp[i-1][j+1];
            
            dp[i][j] =  max(left,max(mid,right));
        }
    }
    
    int mx = -1e9;
    for(int i=0;i<m;i++)
    {
        mx = max(mx,dp[n-1][i]);
    }   
    return mx;
}
```

## 1) Space Optimization
- In this solution we simply make prev and curr array.
- As we need only need left,mid and right value.

```C++
int getMaxPathSum(vector<vector<int>> &mat)
{
    int n = mat.size();
    int m = mat[0].size();
    vector<int> prev(m,-1);
    for(int i=0;i<m;i++)
    {
        prev[i] = mat[0][i];
    }
    
    for(int i=1;i<n;i++)
    {
        vector<int> curr(m,-1);
        for(int j=0;j<m;j++)
        {
            int left = -1e9,right = -1e9;
            if(j>0)
               left = mat[i][j] + prev[j-1];
            int mid = mat[i][j] + prev[j];
            if(j+1 < m)
               right = mat[i][j] + prev[j+1];
            
            curr[j] =  max(left,max(mid,right));
        }
        prev = curr;
    }
    
    int mx = -1e9;
    for(int i=0;i<m;i++)
    {
        mx = max(mx,prev[i]);
    }   
    return mx;
}
```

