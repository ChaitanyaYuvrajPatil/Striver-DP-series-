# Leacture 54

Problem :  Count Square Submatrices with all Ones (Code Studio)

Problem link : https://bit.ly/3tYAUY7


## 2) Using Tabulation

- In this problem we are finding number of square contain only one.
- First we create the dp grid of size same as given array.
- We fill first row and column same as given array.
- Then we simply traverse lop from 1 to n and 1 to m. If if(arr[i][j]==0) then put dp[i][j]=0.
- Else put dp[i][j] = min(dp[i-1][j-1], min(dp[i-1][j], dp[i][j-1])) + 1.
- Finally return sum of all element in dp grid.

```C++
int countSquares(int n, int m, vector<vector<int>> &arr) {
    vector<vector<int>> dp(n, vector<int>(m, 0));

    for(int i=0;i<n;i++) dp[i][0] = arr[i][0];
    for(int j=0;j<m;j++) dp[0][j] = arr[0][j];

    for(int i=1;i<n;i++){
        for(int j=1;j<m;j++){
            if(arr[i][j]==0) dp[i][j]=0;
            else {
                dp[i][j] = min(dp[i-1][j-1], min(dp[i-1][j], dp[i][j-1])) + 1;
            }
        }
    }

    int sum = 0;

    for(int i=0;i<n;i++){
        for(int j=0;j<m;j++){
            sum += dp[i][j];
        }
    }
    return sum;
}

```
