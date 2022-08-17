# Leacture 40
Problem : Best Time to Buy and Sell Stock with Transaction Fee (Code Studio)

Problem link : https://bit.ly/3nZucNH

## 1) Using Memoization 
- Same as DP 36. We only have to reduce fee after selling in this problem.

```C++
int maximumProfit(int n, int fee, vector<int> &prices) {
    vector<vector<int>> dp(n+1,vector<int>(2,0));
   
    for(int ind = n-1;ind>=0; ind--)
    {
        for(int buy=0;buy<=1;buy++)
        {
            if(buy == 1)
            {
                dp[ind][buy] =  max(-prices[ind] + dp[ind+1][0], 0 + dp[ind+1][1]);
            }
            else
            {
                dp[ind][buy] =  max(prices[ind] - fee + dp[ind+1][1], 0 + dp[ind+1][0]);
            }
        }
    }
    return dp[0][1];
}
```

## 2) Using Tabulation

```C++
 int stockProfit(vector<int> &prices){
    int n = prices.size();
    
    vector<vector<int>> dp(n+2,vector<int>(2,0));
    
    for(int ind = n-1;ind>=0; ind--)
    {
        for(int buy = 0;buy<=1;buy++)
        {
            if(buy == 1)
            {
               dp[ind][buy] =  max(-prices[ind] + dp[ind+1][0], 0 + dp[ind+1][1]);
            }
            else
            {
               dp[ind][buy] =  max(prices[ind] + dp[ind+2][1],
                                     0 + dp[ind+1][0]);
            }
        }
    }
    
    return dp[0][1];
}
```

## 3) Using Space Optimization

```C++
int stockProfit(vector<int> &prices){
    int n = prices.size();
    vector<int>front2(2,0);
    vector<int>front1(2,0);
    vector<int>curr(2,0);
    
    for(int ind = n-1;ind>=0; ind--)
    {
        for(int buy = 0;buy<=1;buy++)
        {
            if(buy == 1)
            {
               curr[buy] =  max(-prices[ind] + front1[0], 0 + front1[1]);
            }
            else
            {
               curr[buy] =  max(prices[ind] + front2[1],
                                     0 + front1[0]);
            }
        }
        front2 = front1;
        front1 = curr;
    } 
    return curr[1];
}
```
