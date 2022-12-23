# Merge Two Sorted Lists II | Interviewbit

Created: May 16, 2022 5:05 PM
URL: https://www.interviewbit.com/problems/merge-two-sorted-lists-ii/

Given two sorted integer arrays A and B, merge B into A as one sorted array.

> 
> 
> 
> **Note**: You have to modify the array A to contain the merge of A and B. Do not output anything in your code. **TIP**: C users, please malloc the result into a new array and return the result.
> 

If the number of elements initialized in A and B are `m` and `n` respectively, the resulting size of array A after your code is executed should be `m + n`

**Example :**

```
Input :
         A : [1 5 8]
         B : [6 9]

Modified A : [1 5 6 8 9]

```

```python
void Solution::merge(vector<int> &A, vector<int> &B) {
    // Do not write main() function.
    // Do not read input, instead use the arguments to the function.
    // Do not print the output, instead return values as specified
    // Still have a doubt. Checkout www.interviewbit.com/pages/sample_codes/ for more details
    vector<int> a = A;
    int t = A.size();
    int p = B.size();
    int l = t + p;
    int i =0, j=0;
    for(int k=0; k<l; k++){
        if(i>=t){
            A.push_back(B[j]);
            j++;
        }
        else if(j>=p){
            if(k<t){
                A[k] = a[i];
            }
            else{
                A.push_back(a[i]);
            }  
            i+=1;
        }
        else if(a[i]<=B[j]){
            if(k<t){

                A[k] = a[i];
            }
            else{
                A.push_back(a[i]);
            } 
            i++;
        }
        else if(a[i]>B[j]){
             if(k<t){
                A[k] = B[j];
            }
            else{
                A.push_back(B[j]);
            } 
            j++;
        }
    }
}
```