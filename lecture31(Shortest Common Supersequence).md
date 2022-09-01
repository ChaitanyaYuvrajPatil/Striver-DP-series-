# Leacture 31
Problem : Shortest Common Supersequence (Code studio)

Problem link : https://bit.ly/3vEYKce

## 2) Using Tabulation
- This problem is similar to printing longest common subsequence.
- In this when we traversing back we have to add string varible.
- When letter in both string matches add only one letter else add remaining as given in following code.


```C++
#include<bits/stdc++.h>
string shortestSupersequence(string s, string t)
{
	int m = s.size();
    int n = t.size();
    vector<vector<int>> dp(m+1,vector<int>(n+1,0));
    
    for(int i=0;i<=m;i++) dp[i][0] = 0;
    for(int j=0;j<=n;j++) dp[0][j] = 0;
    
    for(int i=1; i<=m; i++)
    {
        for(int j=1; j<=n; j++)
        {
            if(s[i-1] == t[j-1]) 
                dp[i][j] = 1 +  dp[i-1][j-1]; 
            else
                dp[i][j] = 0 + max(dp[i-1][j],dp[i][j-1]);
        }
    }
    
    string ans = "";
    int i = m;
    int j = n;
    
    while(i>0 && j>0)
    {
        if(s[i-1] == t[j-1])
        {
            ans += s[i-1];
            i--;
            j--;
        }
        else if(dp[i-1][j] > dp[i][j-1])
        {
            ans += s[i-1];
            i--;
        }else
        {
            ans += t[j-1];
            j--;
        }
    }
    
    while(i>0)
    {
        ans += s[i-1];
        i--;
    }
    while(j>0)
    {
        ans += t[j-1];
        j--;
    }
    
    reverse(ans.begin(),ans.end()); 
    return ans;
}
```



