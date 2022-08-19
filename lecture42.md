# Leacture 42
Problem : Printing Longest Increasing Subsequence (Code Studio)

Problem link : https://bit.ly/3rVoIoq

## 1) Space Optimize
- Space optimization approch as use in previous lecture.

```C++
#include<bits/stdc++.h>
int longestIncreasingSubsequence(int arr[], int n)
{
    vector<int>dp(n,1),hash(n);
    int mx = 1;
    int last_ind = 0;
    for(int ind=0;ind<n;ind++)
    {
        for(int prev=0;prev<ind;prev++)
        {
            if(arr[ind] > arr[prev] && 1 + dp[prev] > dp[ind])
            {
                 dp[ind] = 1 + dp[prev];
                 hash[ind] = prev;
            }
        }
        if(dp[ind] > mx)
        {
            mx = dp[ind];
            last_ind = ind;
        }
    }  
    vector<int>temp;
    temp.push_back(arr[last_ind]);
    while(hash[last_ind] != last_ind)
    {
        last_ind = hash[last_ind];
        temp.push_back(arr[last_ind]);
    }
    reverse(temp.begin(),temp.end());
    for(auto it : temp) cout<<it<<" ";
    cout<<endl;
    return mx;
}

```
