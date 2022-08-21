# Leacture 52
Problem : Evaluate Boolean Expression to True (Code Studio)

Problem link : [https://bit.ly/3Kgck9N](https://bit.ly/32tAMUW)

## 1) Using Memoization 


```C++
#include<bits/stdc++.h>
#define ll long long
#define mod 1000000007

ll fun(int i,int j,int isTrue,string & exp,vector<vector<vector<ll>>> &dp)
{
    if(i>j) return 0;
    
    if(i==j)
    {
        if(isTrue)
            return exp[i] == 'T';
        else
            return exp[i] == 'F';
    }
    
    if(dp[i][j][isTrue] != -1) return dp[i][j][isTrue];
    
    
    ll ways = 0;
    
    for(int ind = i+1;ind<=j-1;ind+=2)
    {
        ll lT = fun(i,ind-1,1,exp,dp);
        ll lF = fun(i,ind-1,0,exp,dp);
        ll rT = fun(ind+1,j,1,exp,dp);
        ll rF = fun(ind+1,j,0,exp,dp);
        
        if(exp[ind] == '&')
        {
            if(isTrue) ways = (ways + (rT*lT) % mod)%mod;
            else
                ways = (ways + (rT*lF)%mod + (rF*lT)%mod + (rF*lF)%mod) % mod;
        }
        else if(exp[ind] == '|')
        {
            if(isTrue)
            {
                ways = (ways + (lT*rT)%mod + (lT*rF)%mod + (lF*rT)%mod) % mod;
            }
            else{
                ways = (ways + (rF*lF)%mod) % mod;
            }
        }
        else{
            if(isTrue)
            {
                ways = (ways + (lT*rF)%mod + (lF*rT)%mod) % mod;
            }
            else{
                ways = (ways + (lT*rT)%mod + (lF*rF)%mod) % mod;
            }
        }
    }
    return dp[i][j][isTrue] =  ways;
}
int evaluateExp(string & exp) {
    int n = exp.size();
    vector<vector<vector<ll>>> dp(n,vector<vector<ll>>(n,vector<ll>(2,-1)));
    return fun(0,n-1,1,exp,dp);
}
```
