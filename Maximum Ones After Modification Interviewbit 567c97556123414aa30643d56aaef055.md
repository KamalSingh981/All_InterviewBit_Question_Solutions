# Maximum Ones After Modification | Interviewbit

Created: June 12, 2022 10:00 PM
Tags: Two pointers
URL: https://www.interviewbit.com/problems/maximum-ones-after-modification/

**Problem Description**

Given a binary array **A** and a number **B**, we need to find length of the longest **subsegment** of **‘1’s** possible by changing at most **B** **‘0’s**.

**Problem Constraints**

**Input Format**

First argument is an binary array **A**.

Second argument is an integer **B**.

**Output Format**

Return a single integer denoting the length of the longest **subsegment** of **‘1’s** possible by changing at most **B** **‘0’s**.

**Example Input**

Input 1:

```
 A = [1, 0, 0, 1, 1, 0, 1]
 B = 1

```

Input 2:

```
 A = [1, 0, 0, 1, 0, 1, 0, 1, 0, 1]
 B = 2

```

**Example Output**

**Example Explanation**

Explanation 1:

```
 Here, we should only change 1 zero(0). Maximum possible length we can get is by changing the 3rd zero in the array,
 we get a[] = {1, 0, 0, 1, 1, 1, 1}

```

Explanation 2:

```
 Here, we can change only 2 zeros. Maximum possible length we can get is by changing the 3rd and 4th (or) 4th and 5th zeros.

```

```cpp
int Solution::solve(vector<int> &A, int B) {
    int i = 0;
    int j= 0;
    int ans = 0;
    int flip = 0;
    int n = A.size();
    while(i<n){
        if(A[i]==0){
            flip++;
        }
        if(flip>B){
            if(A[j]==0){
                flip--;
            }
            j++;
        }
        ans =max(ans, i-j+1);
        i++;
    }
    return ans;
}
```

### Algorithm

It uses a method called sliding window in a continuous segment shifted over the entire array.