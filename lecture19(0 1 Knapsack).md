# Leacture 19
Problem : 0/1 Knapsack (Code studio)

Problem link : https://bit.ly/3KHpP3v

## 1) Using Memoization
- In this problem we checking every posibility by Using take and not_take method.
- We taverse from back.
- In base case we only take value at index when weight[ind] <= w) else return 0.
- we return max of take and not_take.

```C++
#include<bits/stdc++.h>
int fun(int ind,int w,vector<int> &weight, vector<int> &value,vector<vector<int>> &dp)
{
    if(ind == 0)
    {
        if(weight[ind] <= w) return value[ind];
        else return 0;
    }
    
    if(dp[ind][w] != -1) return dp[ind][w];
    
    int not_take = fun(ind-1,w,weight,value,dp);
    int take = INT_MIN;
    if(weight[ind] <= w)
        take = value[ind] + fun(ind-1,w - weight[ind],weight,value,dp);
    dp[ind][w]= max(not_take,take);
}

int knapsack(vector<int> weight, vector<int> value, int n, int maxWeight) 
{
	vector<vector<int>> dp(n,vector<int>(maxWeight+1,-1));
    return fun(n-1,maxWeight,weight,value,dp);
}
```

## 1) Using Tabulation

```C++
int knapsack(vector<int> weight, vector<int> value, int n, int maxWeight) 
{
	vector<vector<int>> dp(n,vector<int>(maxWeight+1,0));
    
    for(int i = weight[0]; i<=maxWeight; i++)
    {
        dp[0][i] = value[0];
    }
    
    for(int ind=1;ind<n;ind++)
    {
        for(int w =0;w <= maxWeight; w++)
        {
            int not_take = dp[ind-1][w]; 
            int take = INT_MIN;
            if(weight[ind] <= w)
                take = value[ind] + dp[ind-1][w-weight[ind]];   
            dp[ind][w]= max(not_take,take);
        }
    }
    return dp[n-1][maxWeight]; 
}
```

## 1) Using Space Optimization

```C++
int knapsack(vector<int> weight, vector<int> value, int n, int maxWeight) 
{
    vector<int> prev(maxWeight+1,0),curr(maxWeight+1,0);
    for(int i = weight[0]; i<=maxWeight; i++)
    {
        prev[i] = value[0];
    }
    
    for(int ind=1;ind<n;ind++)
    {
        for(int w =0;w <= maxWeight; w++)
        {
            int not_take = prev[w]; 
            int take = INT_MIN;
            if(weight[ind] <= w)
                take = value[ind] + prev[w-weight[ind]];   
            curr[w]= max(not_take,take);
        }
        prev = curr;
    }
    return prev[maxWeight]; 
}
```

