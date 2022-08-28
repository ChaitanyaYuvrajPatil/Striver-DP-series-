# Leacture 15

Problem : Partition Equal Subset Sum (Code studio)

Problem link : https://bit.ly/34iIIsH

## 1) Using Memoization
- As we know we divide into Equal Subset Sum only when both subset havig equal sum.
- We divide only if sum of element in array divide into equal sum. if not we return false.
- Then return true if we find any subset with sum equla to sum of element in array.
- All other logic same as Leacture 14.

```C++
int fun(int ind,int tar,vector<int> &arr,vector<vector<int>> &dp)
{
    if(tar == 0) return true;
    
    if(ind == 0) return arr[0] == tar;
    
    if(dp[ind][tar] != -1) return dp[ind][tar];
    
    bool not_take = fun(ind-1,tar,arr,dp);
    bool take = false;
    
    if(arr[ind] <= tar)
        take = fun(ind-1,tar-arr[ind],arr,dp);
    
    return dp[ind][tar] =  not_take || take;
}

bool canPartition(vector<int> &arr, int n)
{
	int total_sum = 0;
    for(auto i : arr) total_sum += i;
    
    if(total_sum % 2) return false;
    
    int k = total_sum / 2;
    vector<vector<int>> dp(n,vector<int>(k+1,-1));
    return fun(n-1,k,arr,dp);
}
```

## 1) Using Tabulation
- As we know we divide into Equal Subset Sum only when both subset havig equal sum.
- We divide only if sum of element in array divide into equal sum. if not we return false.
- Then return true if we find any subset with sum equla to sum of element in array.
- All other logic same as Leacture 14.

```C++
bool canPartition(vector<int> &arr, int n)
{
	int total_sum = 0;
    for(auto i : arr) total_sum += i;
    
    if(total_sum % 2) return false;
    
    int k = total_sum / 2;
    vector<vector<bool>> dp(n,vector<bool>(k+1,0));
    
    for(int i=0;i<n;i++) dp[i][0] = true;
    dp[0][arr[0]] = true;
    
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
    return dp[n-1][k];
}

```

## 1) Using Space Optimization
- As we know we divide into Equal Subset Sum only when both subset havig equal sum.
- We divide only if sum of element in array divide into equal sum. if not we return false.
- Then return true if we find any subset with sum equla to sum of element in array.
- All other logic same as Leacture 14.

```C++
bool canPartition(vector<int> &arr, int n)
{
	int total_sum = 0;
    for(auto i : arr) total_sum += i;
    
    if(total_sum % 2) return false;
    
    int k = total_sum / 2;
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
    return prev[k];
}
```

