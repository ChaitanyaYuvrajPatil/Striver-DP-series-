# Leacture 14

Problem : Subset Sum Equal To K (Code studio)

Problem link : https://bit.ly/3ukNmRZ

## 1) Using Memoization
- In this problem we use take and not take technique and store states in dp grid.
- We traverse from bottom to top.
- In recursion we return true when target becomes 0 and store the state.
- Also when we reach to last index return true if arr[0] == tar else return false.
- Then we find take and not take and return and store or of take and not take.

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

bool subsetSumToK(int n, int k, vector<int> &arr) {
    
    vector<vector<int>> dp(1001,vector<int>(1001,-1));
    return fun(n-1,k,arr,dp);
}
```

## 1) Using Tabulation
- In this we declare dp array.
- We traverse from top to bottom.
- We make all space as true from 0 to n in dp[i][0].
- Also we declare dp[0][arr[0]] = true.
- In following loop we calculate take and not_take. 
- Return and store or of take and not take.

```C++
bool subsetSumToK(int n, int k, vector<int> &arr) {
    
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
- In this we declare prev and curr array.
- Make prev[0] = cur[0] = true also  prev[arr[0]] = true.
- In following loop we calculate take and not_take. 
- Return and store or of take and not take.
- Make prev = curr after inner loop ends.

```C++
bool subsetSumToK(int n, int k, vector<int> &arr) {
   
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

