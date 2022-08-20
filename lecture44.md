# Leacture 44
Problem : Divisible Set (Code Studio)

Problem link : https://bit.ly/3rON1Ef

## 1) Using Memoization 
- Same as printing longest incerasing subsequene.
- Just changing few things like sort array and (arr[ind] % arr[prev] == 0)

```C++
#include<bits/stdc++.h>
vector<int> divisibleSet(vector<int> &arr){
    int n = arr.size();
    sort(arr.begin(),arr.end());
    vector<int>dp(n,1),hash(n);
    int mx = 1;
    int last_ind = 0;
    for(int ind=0;ind<n;ind++)
    {
        hash[ind] = ind;
        for(int prev=0;prev<ind;prev++)
        {
            if((arr[ind] % arr[prev] == 0) && 1 + dp[prev] > dp[ind])
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

    return temp;
}
```
