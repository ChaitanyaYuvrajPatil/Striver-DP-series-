# Leacture 6

Problem : House Robber II

## 1) Space Optimize Solution
- logic of function same as L5 solution
- In this Problem given houses are in circle 1st and last house are nabuor.And robber can nor rob adjecent house.
- we make two arrays one with no first element and other with no last element.
- Then take max of maximum sum of adjecent element of two arrays.(Previous Problem)


```C++
long long int robber(vector<int> &nums){
    int n = nums.size();
    
    long long int prev1 = 0;
    long long int prev2 = 0;
    
    for(int i=0;i<n;i++)
    {
        long long int peak = nums[i] + prev2;
        long long int no_peak = prev1;
        long long int curr = max(peak,no_peak);
        
        prev2 = prev1;
        prev1 = curr;
    }   
    return prev1;
}
long long int houseRobber(vector<int>& valueInHouse)
{
    long long int n = valueInHouse.size();
    if(n==1) return valueInHouse[0];
    vector<int>temp1,temp2;
    for(int i=0;i<n;i++)
    {
        if(i != 0) temp1.push_back(valueInHouse[i]);
        if(i != n-1) temp2.push_back(valueInHouse[i]);
    }  
    return max(robber(temp1),robber(temp2));
}

```

