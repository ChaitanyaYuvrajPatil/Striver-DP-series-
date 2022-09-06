# Leacture 46
Problem : Longest Bitonic Sequence (Code Studio)

Problem link : https://bit.ly/3r4o1JB

## 1) Using 
- In this problem we simply calculating LIS from start to end(dp1 array).
- And once again calculating LIS from end to start (dp2 array).
- calculate max of dp1[i] + dp2[i] -1 and return it.

```C++
#include<bits/stdc++.h>

int longestBitonicSequence(vector<int>& arr, int n) {
    vector<int> dp1(n,1);
   
    for(int ind=0;ind<n;ind++)
    {
        for(int prev=0;prev<ind;prev++)
        {
            if(arr[prev] < arr[ind] && 1 + dp1[prev] > dp1[ind])
                dp1[ind] = 1 + dp1[prev];
        }
    }
    
    vector<int> dp2(n,1);
    
    for(int ind=n-1;ind>=0;ind--)
    {
        for(int prev=n-1;prev>ind;prev--)
        {
            if(arr[prev] < arr[ind] && 1 + dp2[prev] > dp2[ind])
                dp2[ind] = 1 + dp2[prev];
        }
    }
    int mx = 0;
    for(int i=0;i<n;i++)
    {
        mx = max(mx,dp1[i] + dp2[i] -1);
    }
    return mx;
} 

```
