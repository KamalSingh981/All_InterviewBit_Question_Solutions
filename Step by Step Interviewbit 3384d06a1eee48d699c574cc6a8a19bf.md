# Step by Step | Interviewbit

Created: May 14, 2022 7:50 PM
URL: https://www.interviewbit.com/problems/step-by-step/

**Problem Description**

Given a **target A** on an infinite number line, i.e. **-infinity to +infinity**.
 You are currently at position **0** and you need to reach the target by moving according to the below rule:

- In **ith** move you can take **i** steps forward or backward.

Find the **minimum** number of moves required to reach the target.

**Problem Constraints**

**Input Format**

First and only argument is an integer A.

**Output Format**

Return an integer denoting the minimum moves to reach target.

**Example Input**

**Example Output**

**Example Explanation**

Explanation 1:

```
 On the first move we step from 0 to 1.
 On the second step we step from 1 to 3.
```

Explanation 2:

```
 On the first move we step from 0 to 1.
 On the second move we step  from 1 to -1.
 On the third move we step from -1 to 2.
```

```cpp
int reachtarget(int target){
    target = abs(target);

    int sum =0, step = 0;
    while (sum <target || (sum - target)%2 !=0){
        step++;
        sum += step;
    }
    return step;
}

int Solution::solve(int A) {
    return reachtarget(A);
}
```