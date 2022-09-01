# Leacture 33
Problem : Edit Distance (Code Studio)

Problem link : https://bit.ly/3HcTJdy

## 1) Using Memoization 
- In this we have to tell minimum number of operation to perform(where oprations are insert,delete,replace).
- In base case if i< 0 return j+1(when first string is empty we have to add j+1 elements).
- In base case if j< 0 return i+1(when second string is empty we have to delete i+1 elements).
- when s1[i] == s2[j] we return and store fun(i-1,j-1,s1,s2,dp).(As we not performing any oprations).
- In else part 1) When we insert one we move back in s2.
               2) When we delete one we move base in s1.
               3) When we replace one we move back in both s1 and s2.
- As we perform above operation we return minimum of this plus one.

```C++
int fun(int i,int j,string &s1, string &s2,vector<vector<int>> &dp)
{
    if(i<0) return j+1;
    if(j<0) return i+1;
    
    if(dp[i][j] != -1) return dp[i][j];
    
    if(s1[i] == s2[j])
    {
        return dp[i][j] = fun(i-1,j-1,s1,s2,dp);
    } 
    else{
        return dp[i][j] = 1 + min(fun(i,j-1,s1,s2,dp),
                       min(fun(i-1,j,s1,s2,dp),
                           fun(i-1,j-1,s1,s2,dp)));
    }
}

int editDistance(string s1, string s2)
{
    int n = s1.size();
    int m = s2.size();
    
    vector<vector<int>> dp(n,vector<int>(m,-1));
    return fun(n-1,m-1,s1,s2,dp);
}
```
### Or (Using one base indexing)
```C++
int fun(int i,int j,string &s1, string &s2,vector<vector<int>> &dp)
{
    if(i==0) return j;
    if(j==0) return i;
    
    if(dp[i][j] != -1) return dp[i][j];
    
    if(s1[i-1] == s2[j-1])
    {
        return dp[i][j] = fun(i-1,j-1,s1,s2,dp);
    } 
    else{
        return dp[i][j] = 1 + min(fun(i,j-1,s1,s2,dp),
                       min(fun(i-1,j,s1,s2,dp),
                           fun(i-1,j-1,s1,s2,dp)));
    }
}

int editDistance(string s1, string s2)
{
    int n = s1.size();
    int m = s2.size();
    
    vector<vector<int>> dp(n+1,vector<int>(m+1,-1));
    return fun(n,m,s1,s2,dp);
}
```

## 2) Using Tabulation

```C++
int editDistance(string s1, string s2)
{
    int n = s1.size();
    int m = s2.size();
    
    vector<vector<int>> dp(n+1,vector<int>(m+1,0));
    
    for(int i=0;i<=n;i++) dp[i][0] = i;
    for(int j=0;j<=m;j++) dp[0][j] = j;
    
    for(int i=1;i<=n;i++)
    {
        for(int j=1;j<=m;j++)
        {
            if(s1[i-1] == s2[j-1])
            {
               dp[i][j] = dp[i-1][j-1]; 
            } 
            else{
               dp[i][j] = 1 + min(dp[i][j-1],
                                       min(dp[i-1][j],
                                            dp[i-1][j-1]));
            }
        }
    }
    return dp[n][m];
}
```

## 3) Using Space Optimization

```C++
int editDistance(string s1, string s2)
{
    int n = s1.size();
    int m = s2.size();
    
    vector<int>prev(m+1,0),curr(m+1,0);
    
    for(int j=0;j<=m;j++) prev[j] = j;
    
    for(int i=1;i<=n;i++)
    {
        curr[0] = i;
        for(int j=1;j<=m;j++)
        {
            if(s1[i-1] == s2[j-1])
            {
               curr[j] = prev[j-1]; 
            } 
            else{
               curr[j] = 1 + min(curr[j-1],
                                       min(prev[j],
                                            prev[j-1]));
            }
        }
        prev = curr;
    }
    return prev[m];
}
```
