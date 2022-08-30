# Leacture 27
Problem : Longest Common Substring (Code studio)

Problem link : https://bit.ly/3H2M3KS

## 1) Using Tabulation

```C++
int lcs(string &str1, string &str2){
    int m = str1.size();
    int n = str2.size();
    
	vector<vector<int>> dp(m+1,vector<int>(n+1,-1));
    int mx = 0;
    
    for(int i=0;i<=m;i++) dp[i][0] = 0;
    for(int j=0;j<=n;j++) dp[0][j] = 0;
    
    for(int i=1;i<=m;i++)
    {
        for(int j=1;j<=n;j++)
        {
            if(str1[i-1] == str2[j-1])
            {
                dp[i][j] = 1 + dp[i-1][j-1]; 
                mx = max(mx,dp[i][j]);
            }
            else 
                dp[i][j] = 0;
        }
    }
    return mx;
}
```

## 2) Using Space Optimization

```C++
int lcs(string &str1, string &str2){
    int m = str1.size();
    int n = str2.size();
    
	vector<vector<int>> dp(m+1,vector<int>(n+1,-1));
    vector<int> prev(n+1,0),curr(n+1,0);
    int mx = 0;
    
    for(int i=1;i<=m;i++)
    {
        for(int j=1;j<=n;j++)
        {
            if(str1[i-1] == str2[j-1])
            {
                curr[j] = 1 + prev[j-1]; 
                mx = max(mx,curr[j]);
            }
            else 
                curr[j] = 0;
        }
        prev = curr;
    }
    return mx;
}
```

