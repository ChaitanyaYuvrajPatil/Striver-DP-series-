# Leacture 7

Problem : Ninja's Training (Code studio)

Problem link : https://www.codingninjas.com/codestudio/problems/ninja-s-training_3621003?leftPanelTab=0

## 1) Using Memoization
- In this problem we first create 2D dp array with row = n and col = 4.
- We write recuring function fun with parameter as day which specify day number,last specify which task performed at last.
- In base case we return max point erned at day 0. when we previously performed last as task.(which we do not include in current max points)
- Similarly we return  max of all task without considering last task.


```C++

int fun(int day, int last, vector<vector<int>> &points,vector<vector<int>>&dp)
{
    if(day == 0)
    {
        int maxi = 0;
        for(int i=0;i<3;i++)
        {
            if(last != i)
                maxi = max(maxi,points[day][i]);
        }
        return maxi;
    }
  
    if(dp[day][last] != -1) return dp[day][last];
    
    int maxi = 0;
    
    for(int i=0;i<3;i++)
    {
        if(i != last)
        {
            int point = fun(day-1,i,points,dp) + points[day][i];
            maxi = max(point,maxi);
        }
    }  
    return dp[day][last] =  maxi;
}

int ninjaTraining(int n, vector<vector<int>> &points)
{
	vector<vector<int>>dp(n,vector<int>(4,-1));
	return fun(n-1,3,points,dp);
}
```

## 2) Using Tabulation
- In this problem we first create 2D dp array with row = n and col = 4.
- As we know in tabulation we traverse from bottom to top. We first take care of base case for day 0.
- We store value like  dp[0][0] = max(points[0][1],points[0][2]) as we choose perform task 0 on day 1,so we can not include dp[0][0] in max.(same for other)
- Then we start loop from day[1] to day[n-1]. Choosing last between 0 to 3.
- Then take max of between all task and store in dp[day][last].


```C++

int ninjaTraining(int n, vector<vector<int>> &points)
{
	vector<vector<int>>dp(n,vector<int>(4,0));
    
    dp[0][0] = max(points[0][1],points[0][2]);
    dp[0][1] = max(points[0][0],points[0][2]);
    dp[0][2] = max(points[0][0],points[0][1]);
    dp[0][3] = max(points[0][0],max(points[0][1],points[0][2]));
    
    for(int day=1;day<n;day++)
    {
        for(int last = 0; last<4;last++)
        {
            int maxi = 0;
            
            for(int task=0;task<3;task++)
            {
                if(last != task)
                    maxi = max(maxi, dp[day-1][task] + points[day][task]);
            }
            dp[day][last] = maxi;
        }
    }
    return dp[n-1][3];
}
```

## 3) Space Optimization
- As we use only previous row data for calculating current data. So we can optimize Space.
- In this we declare prev array of size 4. And we calculate current data use prev array data.
- And store that data in temp array. And make prev = temp;
- Ans return prev[3].

```C++
int ninjaTraining(int n, vector<vector<int>> &points)
{
	vector<int>prev(4,0);
    prev[0] = max(points[0][1],points[0][2]);
    prev[1] = max(points[0][0],points[0][2]);
    prev[2] = max(points[0][0],points[0][1]);
    prev[3] = max(points[0][0],max(points[0][1],points[0][2]));
    
    for(int day=1;day<n;day++)
    {
        vector<int>temp(4,0);
        for(int last = 0; last<4;last++)
        {
            int maxi = 0;
            for(int task=0;task<3;task++)
            {
                if(last != task)
                    maxi = max(maxi, prev[task] + points[day][task]);
            }
            temp[last] = maxi;
        }
        prev = temp;
    }
    return prev[3];
}
```

