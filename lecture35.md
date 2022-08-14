# Leacture 33
Problem : Best Time to Buy and Sell Stock (Code Studio)

Problem link : https://bit.ly/3rN7GIL

## 1) Code
```
#include <bits/stdc++.h> 
int maximumProfit(vector<int> &prices){
    int mn = prices[0], profit =0;
    
    for(int i=1;i<prices.size();i++)
    {
        profit = max(profit,prices[i] - mn);
        mn = min(mn,prices[i]);
    }   
    return profit;
}
```
