# Leacture 3

Problem : Frog Jump

## 1) Using Memoization
- Create dp array of size n+1.
- Write recurrance function base condition if ind = 0 return 0.
- calculate left and right.
- calaculate right only when index > 1 because if we calculate on index 1 it gives negative index.
- return value and store that value in dp array.



```C++
#include<bits/stdc++.h>
int jump(int ind, vector<int> &heights,vector<int> &dp)
{
    if(ind == 0)
        return 0;
    
    if(dp[ind] != -1)
        return dp[ind];
    
    int left = jump(ind-1,heights,dp) + abs(heights[ind]-heights[ind-1]);
    int right = INT_MAX;
    if(ind > 1){
        right = jump(ind-2,heights,dp) + abs(heights[ind]-heights[ind-2]);
    }
    
    return dp[ind] = min(left,right);
}
int frogJump(int n, vector<int> &heights)
{
    
    vector<int>dp(n+1,-1);
    
    return jump(n-1,heights,dp);
}
```


## 2) Using tabulation
- Create dp array of size n+1.
- store dp[0] = 0, as distance of index 0 to 0 is zero.
- calculate left and right
- calaculate right only when index > 1 because if we calculate on index 1 it gives negative index.
- store dp[i] as minimum of left and right.
- return dp[n-1]

```C++
#include<bits/stdc++.h>
int frogJump(int n, vector<int> &heights)
{
    vector<int>dp(n+1,-1);
    dp[0] = 0;
    
    for(int i=1;i<n;i++)
    {
        int left = dp[i-1] + abs(heights[i] - heights[i-1]);
        
        int right = INT_MAX;
        if(i>1)
        {
            right = dp[i-2] + abs(heights[i] - heights[i-2]);
        }
        
        dp[i] = min(left,right);
    }
    
    return dp[n-1];
}
```

## 2) Space Optimization
- Declare prev1 and prev2 as 0.
- Calculate left and right.
- Change value of prev2 and prev2 and prev2 to curr.
- return value of prev1.

```C++
#include<bits/stdc++.h>
int frogJump(int n, vector<int> &heights)
{
    int prev1 = 0;
    int prev2 = 0;
    
    for(int i=1;i<n;i++)
    {
        int left = prev1 + abs(heights[i] - heights[i-1]);
        
        int right = INT_MAX;
        if(i>1)
        {
            right = prev2 + abs(heights[i] - heights[i-2]);
        }
        
        int curr = min(left,right);
        prev2 = prev1;
        prev1 = curr;
    }
    return prev1;
}
```
