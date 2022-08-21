# Leacture 50
Problem : Cost to Cut a Chocolate (Code Studio)

Problem link : https://bit.ly/3rWLMnC

## 1) Using Memoization 

- In this problem we first insert 0 at begin and n at end in cuts array.(we get length of cut by cuts[j+1] - cuts[i-1]).
- Then sort the array.
- In fun() function we are checking every posibility for cuts from i to j.
- In base case if i>j return 0.
- Peacked the minimum and return and store it in dp.

```C++
#include<bits/stdc++.h>
int fun(int i,int j,vector<int> &cuts,vector<vector<int>> &dp)
{
    if(i>j) return 0;
    
    if(dp[i][j] != -1) return dp[i][j];
    
    int mn = 1e9;
    for(int k=i;k<=j;k++)
    {
        int sz = cuts[j+1] - cuts[i-1] + fun(i,k-1,cuts,dp) + fun(k+1,j,cuts,dp);
        mn = min(mn,sz);
    }
    
    return dp[i][j] = mn;
}

int cost(int n, int c, vector<int> &cuts){
    cuts.push_back(n);
    cuts.insert(cuts.begin(),0);
    sort(cuts.begin(),cuts.end());
    
    vector<vector<int>> dp(c+1,vector<int>(c+1,-1));
    return fun(1,c,cuts,dp);
}
```

## 2) Using Tabulation

```C++
 #include<bits/stdc++.h>
 int cost(int n, int c, vector<int> &cuts){
    cuts.push_back(n);
    cuts.insert(cuts.begin(),0);
    sort(cuts.begin(),cuts.end());
    
    vector<vector<int>> dp(c+2,vector<int>(c+2,0));
    
    for(int i=c;i>=1;i--)
    {
        for(int j=1;j<=c;j++)
        {
            if(i>j) continue;
            
            int mn = 1e9;
            for(int k=i;k<=j;k++)
            {
                int sz = cuts[j+1] - cuts[i-1] + dp[i][k-1] + dp[k+1][j];
                mn = min(mn,sz);
            }
    
           dp[i][j] = mn;
        }
    }
    return dp[1][c];
}
```
