# Subarrays with distinct integers! | Interviewbit

Created: June 13, 2022 5:59 PM
Tags: Two pointers
URL: https://www.interviewbit.com/problems/subarrays-with-distinct-integers/

**Problem Description**

Given an array **A** of positive integers,call a (contiguous,not necessarily distinct) subarray of **A** `good` if the number of different integers in that subarray is exactly **B**.

(For example: [1, 2, 3, 1, 2] has 3 different integers 1, 2 and 3)

Return the **number of good subarrays** of **A**.

**Problem Constraints**

1 <= |A| <= 40000

1 <= A[i] <= |A|

1 <= B <= |A|

**Input Format**

The first argument given is the integer array **A**.

The second argument given is an integer **B**.

**Output Format**

Return an integer denoting the **number of good subarrays** of **A**.

**Example Input**

Input 1:

```
 A = [1, 2, 1, 2, 3]
 B = 2

```

Input 2:

```
 A = [1, 2, 1, 3, 4]
 B = 3

```

**Example Output**

**Example Explanation**

Explanation 1:

```
  Subarrays formed with exactly 2 different integers: [1, 2], [2, 1], [1, 2], [2, 3], [1, 2, 1], [2, 1, 2], [1, 2, 1, 2].

```

Explanation 2:

```
  Subarrays formed with exactly 3 different integers: [1, 2, 1, 3], [2, 1, 3], [1, 3, 4].

```

```cpp
int atmost(vector<int> A, int B){
    int ans = 0;
    int i = 0;
    int j = 0;
    unordered_map<int, int> ele;
    while(j<A.size()){
        ele[A[j]]++;
        while(ele.size() > B){
            auto it=ele.find(A[i]);
            it->second--;
            if(it->second ==0)ele.erase(it);
            i++;
        }
        ans += (j - i + 1);
        j++;
    }
    return ans;
}
int Solution::solve(vector<int> &A, int B) {
    if(atmost(A, B) - atmost(A, B-1)+1 < 0){
        return 0;
    }
    return atmost(A, B) - atmost(A, B-1);
}
```

Algorithm 

It uses sliding window method to find the number of subarray having at most B distinct integers in it  and then it subtracts all the subarrays having at most B-1 distinct integers.