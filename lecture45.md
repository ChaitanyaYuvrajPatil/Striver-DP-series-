# Leacture 45
Problem : Longest String Chain (Code Studio)

Problem link : https://bit.ly/3KHsl9J

## 1) Optimize
- Same as longest increasing subsequence problem.
- In this problem we first sort array according to length of string.
- Run loop as per given below.
- In compare function we comparing that prev string is differ by one character with ind string, If yes then dp[ind] = max(dp[prev] + 1,dp[ind]) will execute.
- Return mx.

```C++
#include<bits/stdc++.h>
bool compare(string &s1,string &s2)
{
    if(s1.size() != s2.size() + 1) return false;
    
    int first =0, second=0;
    
    while(first < s1.size())
    {
        if(s1[first] == s2[second])
        {
            first++;
            second++;
        }
        else{
            first++;
        }
    }
    
    return (first == s1.size() && second == s2.size());
}

bool cmp(string &s1,string &s2)
{
    return s1.size() < s2.size();
}
int longestStrChain(vector<string> &arr)
{
    int n = arr.size();
    sort(arr.begin(),arr.end(),cmp);
    vector<int> dp(n,1);
    int mx = 1;
    
    for(int ind = 0;ind<n;ind++)
    {
        for(int prev = 0;prev<ind; prev++)
        {
            if(compare(arr[ind],arr[prev]) && dp[prev] + 1 > dp[ind])
            {
                dp[ind] = max(dp[prev] + 1,dp[ind]);
            }
        }
        mx = max(mx,dp[ind]);
    }
    return mx;
}
```
