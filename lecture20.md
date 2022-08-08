# Leacture 20
Problem : Minimum Elements (Code studio)

Problem link : https://bit.ly/3HJTeIl

## 1) Using Memoization
- In this problem we checking every posibility by Using take and not_take method.
- We taverse from back.
- In base case if tar is divisible by num[0] then only we return tar / num[0], because if not divisible we cannot get coins.
- In take we go to previous index.
- In not_take condition we stand in same index because we may peakup same coin.In next recursion.
- In last we store and return minimum of take and not_take.

```C++
int fun(int ind, int tar,vector<int> &num,vector<vector<int>> &dp)
{
    if(ind == 0)
    {
        if(tar % num[0] == 0) return tar / num[0];
        return 1e9;
    }
    
    if(dp[ind][tar] != -1) return dp[ind][tar];
    
    int not_take = 0 + fun(ind-1,tar,num,dp);
    int take = INT_MAX;
    
    if(num[ind] <= tar) take = 1 + fun(ind,tar-num[ind],num,dp);
    
    return dp[ind][tar] = min(take,not_take);
}
int minimumElements(vector<int> &num, int x)
{
    int n = num.size();
    vector<vector<int>> dp(n,vector<int>(x+1,-1));
    
    int ans =  fun(n-1,x,num,dp);
    
    if(ans >= 1e9) return -1;
    return  ans;
}
```

## 1) Using Tabulation

- We can convert above Memoization into Tabulation in following way.

```C++
int minimumElements(vector<int> &num, int x)
{
    int n = num.size();
    vector<vector<int>> dp(n,vector<int>(x+1,0));
    int target = x;
    for(int tar = 0;tar<=target;tar++)
    {
        if(tar % num[0] == 0) dp[0][tar] =  tar / num[0];
        else dp[0][tar] = 1e9;
    }
    
    for(int ind = 1;ind <n;ind++)
    {
        for(int tar=0;tar<=target;tar++)
        {
            int not_take = 0 + dp[ind-1][tar];
            int take = INT_MAX;
            
            if(num[ind] <= tar) 
                take = 1+dp[ind][tar-num[ind]];
            
            dp[ind][tar] = min(take,not_take);
        }
    }
    int ans =  dp[n-1][target]; 
   
    if(ans >= 1e9) return -1;
    return  ans;
}
```

## 1) Using Space Optimization

```C++
int minimumElements(vector<int> &num, int x)
{
    int n = num.size();
    vector<int> prev(x+1,0),curr(x+1,0);
    
    int target = x;
    for(int tar = 0;tar<=target;tar++)
    {
        if(tar % num[0] == 0) prev[tar] =  tar / num[0];
        else prev[tar] = 1e9;
    }
    
    for(int ind = 1;ind <n;ind++)
    {
        for(int tar=0;tar<=target;tar++)
        {
            int not_take = 0 + prev[tar];
            int take = INT_MAX;
            
            if(num[ind] <= tar) 
                take = 1+curr[tar-num[ind]];
            
            curr[tar] = min(take,not_take);
        }
        prev = curr;
    }
    int ans =  prev[target]; 
   
    if(ans >= 1e9) return -1;
    return  ans;
} 
```

