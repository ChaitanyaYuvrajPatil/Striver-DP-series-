# Leacture 43
Problem : Longest Increasing Subsequence (Code Studio)

Problem link : https://bit.ly/3rVoIoq

## 1) Binary Search
- In this solution we first store first element in temp array.
- Running loop from 1 to n.
- if arr[i] is greater than last element in temp we do temp.push_back(arr[i]);
- Else we find index of lower bound of arr[i] and put arr[i] at that index.
- Finally return size of temp array.

```C++
#include<bits/stdc++.h>
int longestIncreasingSubsequence(int arr[], int n)
{
    vector<int>temp;
    temp.push_back(arr[0]);
    int len = 1;
    
    for(int i=1;i<n;i++)
    {
        if(arr[i] > temp.back())
        {
            temp.push_back(arr[i]);
            len++;
        }
        else
        {
            int ind = lower_bound(temp.begin(),temp.end(),arr[i]) - temp.begin();
            temp[ind] = arr[i];
        }
    }
    return len; //temp.size();
}
```
