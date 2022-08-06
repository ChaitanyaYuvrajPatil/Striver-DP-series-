# Leacture 16

Problem : Partition A Set Into Two Subsets With Minimum Absolute Sum Difference (Code studio)

Problem link : https://bit.ly/3t62bqQ

## 1) Using Memoization
- In this problem we use concept of lecture 14.
- We feel dp grid for all values from 0 to sum of elemnt of array.
- Then we run loop for last row of dp if we find true then we find minimum for two sets.
- return minimum.

```C++
int fun(int ind,int tar,vector<int> &arr,vector<vector<int>> &dp)
{
    if(tar == 0) return dp[ind][tar]=true;
    
    if(ind == 0) return dp[ind][tar] = arr[0] == tar;
    
    if(dp[ind][tar] != -1) return dp[ind][tar];
    
    bool not_take = fun(ind-1,tar,arr,dp);
    bool take = false;
    
    if(arr[ind] <= tar)
        take = fun(ind-1,tar-arr[ind],arr,dp);
    
    return dp[ind][tar] =  not_take || take;
}

int minSubsetSumDifference(vector<int>& arr, int n)
{
    int total_sum = 0;
	for(auto it : arr) total_sum += it;
    int k = total_sum;
    vector<vector<int>> dp(n,vector<int>(k+1,-1));    
    for(int i=0;i<=k;i++)
    {
        bool bl = fun(n-1,i,arr,dp);
    }
    
    int mn = 1e9;
    for(int i=0 ;i<=total_sum;i++)
    {
        if(dp[n-1][i] == 1)
        {
            mn = min(mn, abs((total_sum -i)-i));
        }
    }
    return mn;
}

```

## 1) Using Tabulation
- In this problem we use concept of lecture 14.
- We feel dp grid for all values from 0 to sum of elemnt of array.
- Then we run loop for last row of dp if we find true then we find minimum for two sets.
- return minimum.

```C++
int minSubsetSumDifference(vector<int>& arr, int n)
{
    int total_sum = 0;
	for(auto it : arr) total_sum += it;
    int k = total_sum;
    vector<vector<bool>> dp(n,vector<bool>(k+1,0));
    
    for(int i=0;i<n;i++) dp[i][0] = true;
    if(arr[0] <= k) dp[0][arr[0]] = true;
    
    for(int ind = 1;ind<n;ind++)
    {
        for(int tar = 1;tar<=k;tar++)
        {
            bool not_take = dp[ind-1][tar];
            bool take = false;
            if(arr[ind] <= tar) take = dp[ind-1][tar-arr[ind]];
            dp[ind][tar] = take | not_take;
        }
    }
    
    int mn = 1e9;
    for(int i=0 ;i<=total_sum/2;i++)
    {
        if(dp[n-1][i] == 1)
        {
            mn = min(mn, abs((total_sum -i)-i));
        }
    }
    return mn;
}

```

## 1) Using Space Optimization
- In this problem we use concept of lecture 14.
- We feel dp grid for all values from 0 to sum of elemnt of array.
- Then we run loop for last row of dp if we find true then we find minimum for two sets.
- return minimum.

```C++
int minSubsetSumDifference(vector<int>& arr, int n)
{
    int total_sum = 0;
	for(auto it : arr) total_sum += it;
    int k = total_sum;
    vector<bool>prev(k+1,0),cur(k+1,0);
    
    prev[0] = cur[0] = true;
    prev[arr[0]] = true;
    
    for(int ind = 1;ind<n;ind++)
    {
        for(int tar = 1;tar<=k;tar++)
        {
            bool not_take = prev[tar];
            bool take = false;
            if(arr[ind] <= tar) take = prev[tar-arr[ind]];
            cur[tar] = take | not_take;
        }
        prev = cur;
    }
    
    int mn = 1e9;
    for(int i=0 ;i<=total_sum;i++)
    {
        if(prev[i] == 1)
        {
            mn = min(mn, abs((total_sum -i)-i));
        }
    }
    return mn;
}

```

