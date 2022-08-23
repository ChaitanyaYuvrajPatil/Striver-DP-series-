# Leacture 55

Problem :  Maximum Size Rectangle Sub-matrix With All 1's (Code Studio)

Problem link : https://bit.ly/33HFz61

## 1) Using Memoization 

- Same as Largest Rectangle in Histogram (https://www.youtube.com/watch?v=X0X6G-eWgQ8 && https://www.youtube.com/watch?v=jC_cWLy7jSI)

```C++
#include<bits/stdc++.h>
int largestRectangleArea(vector<int>& histo) {
        
        stack<int> st;
        int maxA = 0;
        
        int n = histo.size();
        
        for(int i =0;i<=n;i++)
        {
            while(!st.empty() && (i==n || histo[st.top()] >= histo[i]))
            {
                int height = histo[st.top()];
                st.pop();
                
                int width;
                
                if(st.empty())
                    width = i;
                else
                    width = i-st.top()-1;
                maxA = max(maxA,width*height);
            }
            st.push(i);
        }
        
        return maxA;
}

int maximalAreaOfSubMatrixOfAll1(vector<vector<int>> &mat, int n, int m){
	int maxArea = 0;
    vector<int> height(m,0);
    
    for(int i=0;i<n;i++)
    {
        for(int j=0;j<m;j++)
        {
            if(mat[i][j] == 1) height[j]++;
            else height[j] = 0;
        }
        
        int area = largestRectangleArea(height);
        maxArea = max(area,maxArea);
    }
    return maxArea;
}
```
