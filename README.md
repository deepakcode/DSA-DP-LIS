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
The idea is to maintain the track of smallest and largest value while traversing input array and keep track of smallest and largest element. if you find any element in between then just update its position in temp array (dp[]) with the help of binary search, because this element is smaller then the largest value it will not increase LIS length but it may update the last element value, which help use to calculate LIS length.

Binary Search (nlogn)

Coding Approach - 
i index means - LIS lenght counter is 'i' and 'i' th index will store last element of increasing subsequence!

<img width="983" alt="Screenshot 2022-08-15 at 2 15 33 AM" src="https://user-images.githubusercontent.com/13814143/184554644-44fe72ac-aec6-4ad1-9230-168a4d0f4a95.png">


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
LIS based questions 

#### Largest Divisible Subset (LIS)

    the only change is  -

    arr[idx] > arr[preIdx

    to 

    (arr[idx] % arr[preIdx) ==0

#### Longest String chain (LIS)

```java


Update this logic in LIS code

boolean checkPossible(String s1, String s2){

    if(s1.length() != s2.length()+1)
        return false;

    int first = 0;
    int second = 0;
    while(first < s1.length()){
        if(s1.charAt(first) == s2.charAt(second)){
            first++;
            second++;
        }else{
            first++;
        }
    }

    if(first == s1.length() &&  second == s2.length())
        return true;
    else
        retur false;
}


boolean compare(String s1, String s2){
    return ;
}

int longestStringChain(String[] arr){

    //First sort the array in based upon string lenght.
    Arrays.sort(arr,(s1,s2)-> s1.length() < s2.length());
    .....
    ....
    ...
}

```



#### Longest Bitonic Subsequence

dp1[]   = 1 , 2 , 2 , 3 , 3 , 4 , 2 , 1

dp2[]   = 1,  5 , 2 , 4 , 3 , 3 , 2 , 1 

bitonic | 1 | 6 | 3 | 6 | 5 | 6 | 3 | 1

bitonic len = 6 

<img width="448" alt="Screenshot 2022-08-15 at 4 04 28 AM" src="https://user-images.githubusercontent.com/13814143/184557319-2fd8917e-ef6b-4afc-84d7-b11da2dc686a.png">



    LIS - > left to right - dp1[i]
    LIS -> Right to left - dp2[i]

    then 
```java

int maxi =0;

for(int i=0; i<n; i++){
    maxi = Math.max(maxi, dp1[i]+dp2[i]-1);
}

return maxi;
```



