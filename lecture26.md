# Leacture 26
Problem : Print Longest Common Subsequence (Code studio)

## 1) Using Tabulation
- In this problem we creating dp grid same as in Lecture 25.
- By using this grid we printing Longest Common Subsequence.
- As we are moving back if s[i-1] == t[j-1] then add letter in ans string s[i-1] or t[j-1].
- Else we move to cell which bigger in between dp[i-1][j], dp[i][j-1].

```C++
#include<bits/stdc++.h>
int lcs(string s, string t)
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
    int i = m, j = n;
    
    while(i>0 && j>0)
    {
        if(s[i-1] == t[j-1])
        {
            ans += s[i-1];
            i--;
            j--;
        }
        else if(dp[i-1][j] > dp[i][j-1])
            i--;
        else
            j--;
    }  
    reverse(ans.begin(),ans.end());
    cout<<ans<<endl;
}
```
