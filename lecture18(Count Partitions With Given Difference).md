# Leacture 18

Problem : Count Partitions With Given Difference (Code studio)

Problem link : https://bit.ly/3r8mG5b

## 1) Using Memoization
- In this problem we use concept of lecture 17.
- In countPartitions function we calculating total sum.
- we know /s1 - s2 = d  and s1 = total - s2, therefore total - 2s2 = d
- s2 = (total-d)/2.  we only have to calculate number of subsets having sum equal to s2.


```C++
int mod = int(1e9 + 7);

int fun(int ind,int target,vector<int> &arr,vector<vector<int>> &dp)
{
    if(ind == 0)
    {
        if(target == 0 && arr[0] == 0) return 2;
        if(target ==0 || arr[0] == target) return 1;
        return 0;
    }
    
    if(dp[ind][target] != -1) return dp[ind][target];
    
    int not_take = fun(ind-1,target,arr,dp);
    int take = 0;
    if(target >= arr[ind])
        take = fun(ind-1,target-arr[ind],arr,dp);
    
    return dp[ind][target] = (not_take + take)%mod;
}

int ways(int n, int sum,vector<int> &arr)
{
    vector<vector<int>> dp(n,vector<int>(sum+1,-1));
    
    return fun(n-1,sum,arr,dp);
}
int countPartitions(int n, int d, vector<int> &arr) {
    
    int total = 0;
    for(auto it : arr) total+=it;

    //s1 - s2 = d  and s1 = total - s2, therefore total - 2s2 = d
    //s2 = (total-d)/2
    
    if(total - d <0 || (total - d)%2) return 0;
    return ways(n,(total - d)/2,arr);
}



```

## 1) Using Tabulation
- In this problem we use concept of lecture 17.
- In countPartitions function we calculating total sum.
- we know /s1 - s2 = d  and s1 = total - s2, therefore total - 2s2 = d
- s2 = (total-d)/2.  we only have to calculate number of subsets having sum equal to s2.

```C++
int mod = int(1e9 + 7);
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

- In this problem we use concept of lecture 17.
- In countPartitions function we calculating total sum.
- we know /s1 - s2 = d  and s1 = total - s2, therefore total - 2s2 = d
- s2 = (total-d)/2.  we only have to calculate number of subsets having sum equal to s2.

```C++
int mod = int(1e9 + 7);
int ways(int n, int target,vector<int> &arr)
{
    vector<int> prev(target+1,0),curr(target+1,0);
    
    if(arr[0] == 0) prev[0] = 2;
    else prev[0] = 1;
    
    if(arr[0] != 0 && arr[0] <= target) prev[arr[0]] = 1;
    
    for(int ind =1;ind<n;ind++)
    {
        for(int sum = 0;sum<=target;sum++)
        {
            int not_take = prev[sum];
            int take = 0;
            if(sum >= arr[ind])
                take = prev[sum - arr[ind]];
    
            curr[sum] = (not_take + take)%mod;
        }
        prev = curr;
    }
    return prev[target];
}
int countPartitions(int n, int d, vector<int> &arr) {
    
    int total = 0;
    for(auto it : arr) total+=it;
    
    if(total - d <0 || (total - d)%2) return 0;
    return ways(n,(total - d)/2,arr);
}

```

