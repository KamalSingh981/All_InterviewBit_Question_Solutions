# 3 Sum Zero | Interviewbit

Created: June 13, 2022 12:56 PM
Tags: Two pointers
URL: https://www.interviewbit.com/problems/3-sum-zero/

Given an array S of n integers, are there elements a, b, c in S such that a + b + c = 0? 
 Find all unique triplets in the array which gives the sum of zero.

**Note:**

> 
> 
> 
> Elements in a triplet (a,b,c) must be in non-descending order. (ie, a ≤ b ≤ c) The solution set must not contain duplicate triplets.
> 
> For example, given array `S = {-1 0 1 2 -1 -4}`,
> 
> A solution set is: `(-1, 0, 1)` `(-1, -1, 2)`
> 

Note:You only need to implement the given function. Do not read input, instead use the arguments to the function. Do not print the output, instead return values as specified. Still have a question? Checkout [Sample Codes](https://www.interviewbit.com/pages/sample_codes/) for more details.

```cpp
vector<vector<int> > Solution::threeSum(vector<int> &A) {
    vector<vector<int>> ans; 
    if(A.size() < 3){
        return ans;
    }
    sort(A.begin(), A.end());
    
    for(int i = 0; i <A.size()-2; i++){
        if(i>0 && A[i] == A[i-1]){
            continue;
        }
        int st = i + 1;
        int en = A.size() - 1;
        while(st<en){    
            if(en < A.size() - 1 && A[en] == A[en + 1]){
                en--;
                continue;
            }
            long long int sum = (long long int)A[i] + (long long int) A[st] + (long long int)A[en];
            if(sum == 0){
                vector<int> tri;
                tri.push_back(A[i]);
                tri.push_back(A[st]);
                tri.push_back(A[en]);
                ans.push_back(tri);
                
                st++; en--;
            }
            else if(sum > 0){
                en--;
            }
            else{
                 st++;
            }      
        }   
    }
    return ans;   
}
```

### Step for solving this problem

1. Sort the array
2. Run the for loop from i = 0 to  i = n - 2 where n is the size of the array.
3. Consider A[i] the smallest element of the triplet and then use two pointer approach to the find two numbers such that there sum is -A[i].
4. Key point to remember here is that during summation int can overflow which leads to wrong result. 
5. Also, take care redundant triplets. This can be easily done by continuing over all the same elements from behind the array.