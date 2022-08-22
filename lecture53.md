# Leacture 53
Problem : Palindrome Partitioning ll (Code Studio)

Problem link : https://bit.ly/3jNRzqX

## 1) Using Memoization 

- In this problem we starting from i and check if string from i to j is palindrome or not.
- If it is Palindrome we add 1 and call fun for next j+1.
- Store minCost and return it.

```C++
#include<bits/stdc++.h>
bool is_palindrome(int i,int j,string str)
{
    while(i<j)
    {
        if(str[i] != str[j]) return false;
        i++;
        j--;
    }
    return true;
}
int fun(int i,int n,string str,vector<int> &dp)
{
    if(i==n) return 0;
    
    if(dp[i] != -1 ) return dp[i];
    
    int minCost = INT_MAX;
    
    for(int j=i;j<n;j++)
    {
        if(is_palindrome(i,j,str))
        {
            int cost = 1 + fun(j+1,n,str,dp);
            minCost = min(minCost,cost);
        }
    }
    
    return dp[i] = minCost;
}

int palindromePartitioning(string str) {
    int n = str.size();
    
    vector<int> dp(n,-1);
    return fun(0,n,str,dp) - 1;
}

```

## 2) Using Tabulation

```C++
#include<bits/stdc++.h>
bool is_palindrome(int i,int j,string str)
{
    while(i<j)
    {
        if(str[i] != str[j]) return false;
        i++;
        j--;
    }
    return true;
}

int palindromePartitioning(string str) {
    int n = str.size();
    
    vector<int> dp(n+1,0);
    
    for(int i=n-1;i>=0;i--)
    {
        int minCost = INT_MAX;
    
        for(int j=i;j<n;j++)
        {
            if(is_palindrome(i,j,str))
            {
               int cost = 1 + dp[j+1]; 
               minCost = min(minCost,cost);
            }
        } 
       dp[i] = minCost;
    }
    return dp[0] - 1;
}

```
