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

Intution : 
Binary Search 


Coding Approach - 
i index means - counter is i and i index will store last element of increasing subsequence.

```java

// Binary search (note boundaries in the caller)
    // A[] is ceilIndex in the caller
    static int CeilIndex(int A[], int l, int r, int key)
    {
        while (r - l > 1) {
            int m = l + (r - l) / 2;
            if (A[m] >= key)
                r = m;
            else
                l = m;
        }

        return r;
    }

    static int LongestIncreasingSubsequenceLength(int A[], int size)
    {
        // Add boundary case, when array size is one

        int[] dp = new int[size];

        int len =1; // always points empty slot
                                                        // int A[] = { 2, 5, 3, 7, 11, 8, 10, 13, 6 };
        dp[0] = A[0];// 0=2

        for (int i = 1; i < size; i++) {

            // 0,0,2,3,

            if (A[i] < dp[0])
                // new smallest value
                dp[0] = A[i];

            else if (A[i] > dp[len - 1])
                // A[i] wants to extend largest subsequence
                dp[len++] = A[i];

            else
                // A[i] wants to be current end candidate of an existing
                // subsequence. It will replace ceil value in dp
                dp[CeilIndex(dp, -1, len - 1, A[i])] = A[i];
        }

        return len;
    }
    
```


