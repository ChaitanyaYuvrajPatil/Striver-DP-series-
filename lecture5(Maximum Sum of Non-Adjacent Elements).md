# Leacture 5

Problem : Maximum Sum of Non-Adjacent Elements (code studio)

## 1) Using Memoization
- Create dp array of size n.
- take base case for ind = 0 return nums[ind].
- Also if index becomes negative return 0.
- calculate peak if we peak current ind.(call function with ind-2 because we do not peak Adjacent Element)
- calculate when we do not peak current ind.
- store and return max of peak and non peak


```C++
int fun(int ind, vector<int> &nums,vector<int> &dp)
{
    if(ind == 0) return nums[ind];
    
    if(ind < 0) return 0;
    
    if(dp[ind] != -1) return dp[ind];
    
    int peak = nums[ind] + fun(ind-2,nums,dp);
    int no_peak = 0 + fun(ind-1,nums,dp);
    
    return dp[ind] = max(peak,no_peak);
}

int maximumNonAdjacentSum(vector<int> &nums){
    int n = nums.size();
    vector<int>dp(n,-1);
    
    return fun(n-1,nums,dp);
}

```


## 2) Using tabulation
- Create dp array of size n.
- declare dp[0] = nums[0].
- Run loop from 1 to n-1. Calculate peak and no_peak.
- Retun dp[n-1].

```C++
int maximumNonAdjacentSum(vector<int> &nums){
    int n = nums.size();
    vector<int>dp(n,-1);
    
    dp[0] = nums[0];
    
    for(int i=1;i<n;i++)
    {
        int peak = nums[i];
        if(i>1)
            peak += dp[i-2];
        int no_peak = 0 + dp[i-1];
        
        dp[i] = max(peak,no_peak);
    }   
    return dp[n-1];
}
```

## 2) Space Optimization
- Declare two variable prev1 = 0 and prev2 = 0.
- Run loop from o to n-1.
- Calculate peak and no_peak. Take their max in variable curr.
- Change prev2 to prev1 and prev1 to curr.
- Retun prev1.

```C++
int maximumNonAdjacentSum(vector<int> &nums){
    int n = nums.size();

    int prev1 = 0;
    int prev2 = 0;
    
    for(int i=0;i<n;i++)
    {
        int peak = nums[i] + prev2;
        int no_peak = prev1;
        int curr = max(peak,no_peak);
        
        prev2 = prev1;
        prev1 = curr;
    }   
    return prev1;
}
```

