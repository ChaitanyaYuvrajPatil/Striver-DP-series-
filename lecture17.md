# Leacture 17

Problem : Counts Subsets with Sum K (Code studio)

Problem link : https://bit.ly/3t62bqQ

## 1) Using Memoization
- In this problem we use concept of lecture 14 of take and not_take. 
- With base case given bellow.
- return sum of take and not_take.

```C++
int fun(int ind, int target, vector<int>& arr, vector<vector<int>> &dp){
    if(ind == 0) {
        if(target == 0 && arr[ind] == 0) return 2;
        if(target == 0 || arr[ind] == target) return 1;
        return 0;
    }
    
    if(dp[ind][target]!=-1)
        return dp[ind][target];
        
    int notTaken = fun(ind-1,target,arr,dp);
    
    int taken = 0;
    if(arr[ind]<=target)
        taken = fun(ind-1,target-arr[ind],arr,dp);
        
    return dp[ind][target]= notTaken + taken;
}

int findWays(vector<int> &num, int k)
{
    int n = num.size();
    vector<vector<int>> dp(n,vector<int>(k+1,-1));
    
    return fun(n-1,k,num,dp);
}
```

## 1) Using Tabulation
- In this problem we use concept of lecture 14.
- We declare dp grid of size nx(target+1)..
- We use take and not_take concept.

```C++
int findWays(vector<int> &num, int tar)
{
    int n = num.size();
    vector<vector<int>> dp(n,vector<int>(tar+1,0));
    
    for(int i=0;i<n;i++)
        dp[i][0] = 1;
    if(num[0] <= tar) dp[0][num[0]] = 1;
    
    for(int ind=1;ind<n;ind++)
    {
        for(int sum = 0;sum<=tar;sum++)
        {
            int not_take = dp[ind-1][sum];
            int take = 0;
            if(num[ind] <= sum)
                take = dp[ind-1][sum - num[ind]];
            dp[ind][sum] = take + not_take;
        }
    }
    
    return dp[n-1][tar];
}
```

## 1) Using Space Optimization


```C++
int findWays(vector<int> &num, int tar)
{
    int n = num.size();
    vector<int>prev(tar+1,0),curr(tar+1,0);
    for(int i=0;i<n;i++)
        prev[0] = 1;
    if(num[0] <= tar) prev[num[0]] = 1;
    
    for(int ind=1;ind<n;ind++)
    {
        for(int sum = 0;sum<=tar;sum++)
        {
            int not_take = prev[sum];
            int take = 0;
            if(num[ind] <= sum)
                take = prev[sum - num[ind]];
            curr[sum] = take + not_take;
        }
        prev = curr;
    }
    return prev[tar];
}

```

