# DSA-DP-LIS

### Longest increasing subsequence -

#### This method is required if you want to print LCS


```java
class Solution 
{
    static int longestSubsequence(int n, int a[]){
        
        return lis(0, -1, a, n);
        
    }
    
    static int lis(int idx, int preIdx, int[] arr, int n){
        
        if(idx >= n)
            return 0; 
       
        int len = 0 + lis(idx+1, preIdx, arr, n); 
       
        if(preIdx == -1 || arr[idx] > arr[preIdx] ){
            len = Math.max(len, 1 + lis(idx+1, idx, arr, n)); //take
        }
        
        return len;
        
    }
} 
```

#### There is another efficient approach is avaiable in less space time complexity, but we can't print LIS from this method, but we can count it.
