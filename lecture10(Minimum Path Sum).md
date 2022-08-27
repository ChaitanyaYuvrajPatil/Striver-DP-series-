# Leacture 10

Problem : Minimum Path Sum (Code studio)

Problem link : https://bit.ly/3q5sqfu

## 1) Using Memoization
- In this problem we have to calculate minimum sum require to reach from grid[0][0] to grid[n-1][m-1].
- In this problem we calculate all possible ways and take their minimum.
- We declare dp grid of size same as size of grid.
- we make base cases as given in code.
- if i<0 or  j<0 we return max value as we calculate minimum.
- We calculate up and left and return minimum of them store in dp[i][j].

```C++
#include<bits/stdc++.h>

int fun(int i,int j,vector<vector<int>> &grid,vector<vector<int>> &dp)
{
    if(i==0 && j==0) return grid[i][j];
    if(i<0 || j<0) return 1e9;
    if(dp[i][j] != -1) return dp[i][j];
    
    int up = grid[i][j] + fun(i-1,j,grid,dp);
    int left = grid[i][j] + fun(i,j-1,grid,dp);
    
    return dp[i][j] = min(up,left); 
}
int minSumPath(vector<vector<int>> &grid) {
    int row = grid.size();
    int col = grid[0].size();
    vector<vector<int>> dp(row,vector<int>(col,-1));  
    return fun(row-1,col-1,grid,dp);
}
```

## 1) Using Tabulation
- In this problem we have to calculate minimum sum require to reach from grid[0][0] to grid[n-1][m-1].
- In this problem we calculate all possible ways and take their minimum.
- We declare dp grid of size same as size of grid.
- We run loop in size of grid. if(i==0 && j==0) dp[i][j] = grid[i][j]. else we calculate take minimum of up and left.


```C++
int minSumPath(vector<vector<int>> &grid) {
    int row = grid.size();
    int col = grid[0].size();
    vector<vector<int>> dp(row,vector<int>(col,-1));  
    
    for(int i=0;i<row;i++)
    {
        for(int j=0;j<col;j++)
        {
            if(i==0 && j==0) dp[i][j] = grid[i][j];
            else
            {
                int left = 1e9,up =1e9;
                if(i>0)
                   up = grid[i][j] + dp[i-1][j];
                if(j>0)
                   left = grid[i][j] + dp[i][j-1];
                
                dp[i][j] = min(up,left);
            }
        }
    }
   return dp[row-1][col-1];
}   
```

## 1) Space Optimization
- In this solution we simply make prev and temp array.
- As we need only need up and left value.

```C++
int minSumPath(vector<vector<int>> &grid) {
    int row = grid.size();
    int col = grid[0].size();
 
    vector<int>prev(col,0);
    for(int i=0;i<row;i++)
    {
        vector<int>temp(col,0);
        for(int j=0;j<col;j++)
        {
            if(i==0 && j==0) temp[j] = grid[i][j];
            else
            {
                int left = 1e9,up =1e9;
                if(i>0)
                   up = grid[i][j] + prev[j];
                if(j>0)
                   left = grid[i][j] + temp[j-1];
                
                temp[j] = min(up,left);
            }
        }
        prev = temp;
    }
   return prev[col-1];
}

```

