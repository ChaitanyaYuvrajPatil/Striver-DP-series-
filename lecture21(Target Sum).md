# Leacture 21
Problem : Target Sum (Code studio)

Problem link : https://bit.ly/3swy5uL

## 1) Using Memoization
- This priblem is exactly same as Leacture 18.
- In this we only have to find number of subsets whose different is target.
- All logic is same.

```C++
int fun(int ind,int tar,vector<int> &arr,vector<vector<int>> &dp)
{
    if(ind == 0)
    {
        if(arr[0] == 0 && tar == 0) return 2;
        if(tar == 0 || arr[0] == tar) return 1;
        return 0;
    }
    
    if(dp[ind][tar] != -1) return dp[ind][tar];
    int not_take = fun(ind-1,tar,arr,dp);
    
    int take = 0;
    if(tar >= arr[ind])
        take = fun(ind-1,tar - arr[ind],arr,dp);
    
    return dp[ind][tar] = take + not_take;
}

int ways(int n, int sum,vector<int> &arr)
{
    vector<vector<int>> dp(n,vector<int>(sum+1,-1));
    
    return fun(n-1,sum,arr,dp);
}

int targetSum(int n, int target, vector<int>& arr) {
    int total = 0;
    for(auto it : arr) total+=it;
    int d = target;
    //s1 - s2 = d  and s1 = total - s2, therefore total - 2s2 = d
    //s2 = (total-d)/2
    
    if(total - d <0 || (total - d)%2) return 0;
    return ways(n,(total - d)/2,arr);
}

```

## 1) Using Tabulation

- This priblem is exactly same as Leacture 18.
- In this we only have to find number of subsets whose different is target.
- All logic is same.

```C++
int ways(int n, int tar,vector<int> &num)
{
    //int n = num.size();
    vector<vector<int>> dp(n,vector<int>(tar+1,0));
    
    if(num[0] == 0) dp[0][0] = 2;
    else dp[0][0] = 1;
    
    if(num[0] != 0 && num[0] <= tar) dp[0][num[0]] =1;
    
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

int targetSum(int n, int target, vector<int>& arr) {
    int total = 0;
    for(auto it : arr) total+=it;
    int d = target;
    //s1 - s2 = d  and s1 = total - s2, therefore total - 2s2 = d
    //s2 = (total-d)/2
    
    if(total - d <0 || (total - d)%2) return 0;
    return ways(n,(total - d)/2,arr);
}

```

## 1) Using Space Optimization

- This priblem is exactly same as Leacture 18.
- In this we only have to find number of subsets whose different is target.
- All logic is same.

```C++
int ways(int n, int tar,vector<int> &num)
{
    
    vector<int>prev(tar+1,0), curr(tar+1,0);
    if(num[0] == 0) prev[0] = 2;
    else prev[0] = 1;
    
    if(num[0] != 0 && num[0] <= tar) prev[num[0]] =1;
    
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

int targetSum(int n, int target, vector<int>& arr) {
    int total = 0;
    for(auto it : arr) total+=it;
    int d = target;
    //s1 - s2 = d  and s1 = total - s2, therefore total - 2s2 = d
    //s2 = (total-d)/2
    
    if(total - d <0 || (total - d)%2) return 0;
    return ways(n,(total - d)/2,arr);
}

```

