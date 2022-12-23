# Distribute Candy | Interviewbit

Created: July 26, 2022 12:40 AM
Tags: GreedyAlgorithm
URL: https://www.interviewbit.com/problems/distribute-candy/

There are **N** children standing in a line. Each child is assigned a rating value.

You are giving candies to these children subjected to the following requirements:

```
1. Each child must have at least one candy.
2. Children with a higher rating get more candies than their neighbors.

```

What is the minimum candies you must give?

**Input Format:**

```
The first and the only argument contains N integers in an array A.

```

**Output Format:**

```
Return an integer, representing the minimum candies to be given.

```

**Example:**

```
Input 1:
    A = [1, 2]

Output 1:
    3

Explanation 1:
    The candidate with 1 rating gets 1 candy and candidate with rating cannot get 1 candy as 1 is its neighbor.
    So rating 2 candidate gets 2 candies. In total, 2 + 1 = 3 candies need to be given out.

Input 2:
    A = [1, 5, 2, 1]

Output 2:
    7

Explanation 2:
    Candies given = [1, 3, 2, 1]

```

```cpp
int Solution::candy(vector<int> &A) {  
    int n = A.size();  
    vector<int> l(n+1, 1);
    for(int i = 1; i<n; i++){
        if(A[i-1] < A[i]){
            l[i] = l[i-1]+1;
        }
    }
    int ans = 0;
    int right = 1;
    for(int i = n-2; i>=0; i--){
        if(A[i+1] < A[i]){
            right++;
            l[i] = max(right, l[i]);
        }
        else{
            right = 1;
        }
    }
    for(auto i:l){
        ans += i;
    }
    return ans-1;
}
```

Without using space

```cpp
int Solution::candy(vector<int> &A) {
    int n = A.size();
    if(n == 0)
     return 0;
    int i = 1;
    int sum = 1;
    int candy = 1;
     while(i < n){
         if(A[i] > A[i - 1]){
             candy++;
             sum += candy;
             i++;
         }else if(A[i -1] > A[i]){
             int count =0;
             while(A[i] < A[i-1] && i < n){
                 count++;
                 i++;
             }
             if(count >= candy){
              sum += count - candy + 1;}
              
              sum += count*(count+1)/2 ;
              candy = 1;
         }else{ // important last block when both have same ranking.
             candy = 1;
             sum += candy;   
             i++;
         }
     }
     
     return sum;
}
```