# Leacture 4

Problem : Frog Jump with k Distances (code studio)

## 1) Using Memoization
- Create dp array of size n+1.
- Write recurrance function base condition if ind = 0 return 0.
- calculate minimum distance by loop through 1 to k.
- calculate cal_min if ind-i >= 0 because ind-i may give negative index.
- return dp[ind] as cal_min.


```C++
int jump(int ind, vector<int> &heights,vector<int> &dp,int k)
{
    if(ind == 0)
        return 0;
    
    if(dp[ind] != -1)
        return dp[ind];

    int cal_min = INT32_MAX;

    for(int i=1;i<=k;i++)
    {
        if(ind-i>=0)
        {
            int left = jump(ind-i,heights,dp,k) + abs(heights[ind]-heights[ind-i]);
            cal_min = min(cal_min,left);
        }
    }
    
    return dp[ind] = cal_min;
}
int frogJump(int n, vector<int> &heights,int k)
{
    
    vector<int>dp(n+1,-1);
    
    return jump(n-1,heights,dp,k);
}

int main() {

  vector<int> height = {30,10,60 , 10 , 60 , 50};
  int n=height.size();
  int k=2;
  vector<int> dp(n,-1);
  cout<<frogJump(n,height,k);
}

```


## 2) Using tabulation

```C++
int frogJump(int n, vector<int> &heights,int k)
{   
    vector<int>dp(n+1,-1);
    dp[0] = 0;
    
    for(int ind = 1;ind < n; ind++)
    {
        int cal_min = INT32_MAX;
        for(int i=1;i<=k;i++)
        {
            if(ind-i >=0)
            {
                int left = dp[ind-i] + abs(heights[ind]-heights[ind-i]);
                cal_min = min(cal_min,left);
            }
        }

        dp[ind] = cal_min;
    }

    return dp[n-1];
}

int main() {

  vector<int> height = {30,10,60 , 10 , 60 , 50};
  int n=height.size();
  int k=2;
  vector<int> dp(n,-1);
  cout<<frogJump(n,height,k);
}
```

