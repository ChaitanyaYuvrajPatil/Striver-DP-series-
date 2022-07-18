# Leacture 1

Problem : fibonacci series 

## 1) Using Memoization
- Create dp array of size n+1
- Write recurrance function 
- And store value of each value calculated in dp array.



```C++
int Fibonacci(int n,vector<int> &dp)
{
   if(dp[n] !=-1)return dp[n];
   if ( n == 0 )
      return 0;
   else if ( n == 1 )
      return 1;
   else
      return dp[n] =  Fibonacci(n-1,dp) + Fibonacci(n-2,dp);
} 
int main()
{
   int n, i = 0, c;
   cin>>n;

   vector<int> dp(n+1,-1);
 
   for ( c = 0 ; c < n ; c++ )
   {
     cout<<Fibonacci(c,dp) << " ";
   }
 
   return 0;
}
```


## 2) Using tabulation
- Create dp array of size n+1
- set value of dp[0] to 0 and dp[1] to 1
- start loop from 2 index upto n
- And store value of dp[i-1] + dp[i-2] in dp[i]

```C++
int main()
{
   int n, i = 0, c;
   cin>>n;

   vector<int> dp(n+1,-1);

   dp[0] = 0;
   dp[1] = 1;

   for(int i=2;i<=n;i++)
   {
      dp[i] = dp[i-1]+dp[i-2];
   }

   for(int i=0;i<n;i++)
   {
      cout<<dp[i]<<" ";
   }
 
   return 0;
}
```
