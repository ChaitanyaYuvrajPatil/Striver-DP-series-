# Leacture 54

Problem :  Partition Array for Maximum Sum (LeetCode)

Problem link : https://leetcode.com/problems/partition-array-for-maximum-sum/

## 1) Using Memoization 

```C++
int fun(int ind,vector<int>& arr, int k,vector<int> &dp)
    {
        int n = arr.size();
        
        if(ind == n) return 0;
        
        if(dp[ind] != -1) return dp[ind];
        
        int len = 0;
        int maxi = INT_MIN;
        int mx_ans = INT_MIN;
        
        for(int j = ind; j< min(ind+k,n);j++)
        {
            len++;
            maxi = max(maxi,arr[j]);
            int sum = len*maxi + fun(j+1,arr,k,dp);
            mx_ans = max(mx_ans,sum);
        }
        
        return dp[ind] = mx_ans;
    }
    
    int maxSumAfterPartitioning(vector<int>& arr, int k) {
        
        int n = arr.size();
        
        vector<int> dp(n,-1);
        
        return fun(0,arr,k,dp);
    }

```

## 2) Using Tabulation

```C++
#include<bits/stdc++.h>
int maxSumAfterPartitioning(vector<int>& arr, int k) {
        
        int n = arr.size();
        
        vector<int> dp(n+1,0);
        
        for(int ind = n-1; ind >= 0; ind--)
        {
            int len = 0;
            int maxi = INT_MIN;
            int mx_ans = INT_MIN;
        
            for(int j = ind; j< min(ind+k,n);j++)
            {
               len++;
               maxi = max(maxi,arr[j]);
               int sum = len*maxi + dp[j+1];
               mx_ans = max(mx_ans,sum);
            }
        
            dp[ind] = mx_ans;
        }
        
        return dp[0];
    }

```
