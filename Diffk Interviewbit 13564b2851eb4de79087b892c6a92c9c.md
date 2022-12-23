# Diffk | Interviewbit

Created: May 17, 2022 1:03 PM
URL: https://www.interviewbit.com/problems/diffk/

Given an array ‘A’ of sorted integers and another non negative integer k, find if there exists 2 indices i and j such that A[i] - A[j] = k, i != j.

> 
> 
> 
> **Example:**
> 
> Input :
> 

> 
> 
> 
> Output : `YES`
> 
> as `5 - 1 = 4`
> 

Return `0 / 1` ( 0 for false, 1 for true ) for this problem

Try doing this in less than linear space complexity.

```cpp
int Solution::diffPossible(vector<int> &A, int B) {
    int a = 0, b =1;
    for(int i=0; i<2*A.size(); i++){
        if(A[b] - A[a] == B && b!=a){
            return 1;
        }
        else if(A[b] - A[a] <= B){
            b += 1;
        }
        else if(A[b]- A[a] >= B){
            a += 1;
        }

    }
    return 0;
}
```