# Leacture 2

Problem : Climbing Stairs 

## 1) Using Memoization
<!-- - Create dp array of size n+1
- Write recurrance function 
- And store value of each value calculated in dp array. -->



```C++
class Solution{
	public:
	
	    int rec(int ind, vector<int>&dp)
	    {
	        if(ind == 0) return 1;
	        if(ind < 0) return 0;
	        
	        if(dp[ind] != -1)
	           return dp[ind]%1000000007;;
	           
	        int left = rec(ind-1,dp)%1000000007;;
	        int right = rec(ind-2,dp)%1000000007;;
	        
	        return dp[ind] = (left+right)%1000000007;;
	    }
		int nthPoint(int n){
		    // Code here
		    vector<int>dp(n+1,-1);
		    
		    return rec(n,dp)%1000000007;;
		}
};
```


## 2) Using tabulation
<!-- - Create dp array of size n+1
- set value of dp[0] to 0 and dp[1] to 1
- start loop from 2 index upto n
- And store value of dp[i-1] + dp[i-2] in dp[i] -->

```C++
class Solution{
	public:
		int nthPoint(int n){
		    int mod = 1e9+7;
		    vector<int> dp(n+1);
		    dp[0] = 1;
		    dp[1] = 1;
		    
		    for(int i=2;i<=n;i++) {
		        dp[i] = (dp[i-1] + dp[i-2])%mod;
		    }
		    return dp[n];
		}
};
```
