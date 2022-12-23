# Sort by Color | Interviewbit

Created: May 17, 2022 12:25 PM
URL: https://www.interviewbit.com/problems/sort-by-color/

Given an array with n objects colored red, white or blue, 
 sort them so that objects of the same color are adjacent, with the colors in the order red, white and blue.

Here, we will use the integers 0, 1, and 2 to represent the color red, white, and blue respectively.

*Note: Using library sort function is not allowed.*

**Example :**

```
Input : [0 1 2 0 1 2]
Modify array so that it becomes : [0 0 1 1 2 2]

```

```python
void Solution::sortColors(vector<int> &A) {
    // Do not write main() function.
    // Do not read input, instead use the arguments to the function.
    // Do not print the output, instead return values as specified
    // Still have a doubt. Checkout www.interviewbit.com/pages/sample_codes/ for more details
    int arr[3] = {0};
    for(int i=0; i<A.size(); i++){
        if(A[i]==0){
            arr[0]+=1;
        }
        else if(A[i]==1){
            arr[1] += 1;
        }
        else{
            arr[2] += 1;
        }
    }
    
    int count =0;
    for(int i=0; i<3; i++){
        for(int j=0; j<arr[i]; j++){
            A[count] = i;
            count += 1;
        }
        
    }
}
```