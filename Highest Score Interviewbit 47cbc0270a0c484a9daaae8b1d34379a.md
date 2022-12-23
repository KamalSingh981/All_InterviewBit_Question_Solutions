# Highest Score | Interviewbit

Created: May 10, 2022 7:06 PM
URL: https://www.interviewbit.com/problems/highest-score/

**Problem Description**

You are given a 2D string array **A** of dimensions **N x 2**,
 where each row consists of two strings: first is the name of the student, second is their marks.

You have to find the maximum average mark. If it is a floating point, round it down to the nearest integer less than or equal to the number.

**Problem Constraints**

**Input Format**

**Output Format**

**Example Input**

Input 1:

```
A = [["Bob", "80"], ["Bob", "90"], ["Alice", "90"]]

```

Input 2:

```
A = [["Bob", "80"], ["Bob", "90"], ["Alice", "90"], ["Alice", "10"]]

```

**Example Output**

Output 1:

```
90

```

Output 2:

```
85

```

**Example Explanation**

Explanation 1:

```
Alice has the highest average with 90 marks.
```

Explanation 2:

```
Bob has the highest average with 85 marks.

```

# Interviewbit Code

```cpp
int Solution::highestScore(vector < vector < string > > & A) {
    map < string, pair < int, int >> mp;
    for (int i = 0; i < A.size(); i++) {
        if (mp.find(A[i][0]) == mp.end()) {
            mp[A[i][0]] = make_pair(0, 0);
        }
        mp[A[i][0]] = make_pair(mp[A[i][0]].first + stoi(A[i][1]), mp[A[i][0]].second + 1);
    }
    int ans = 0;
    for (auto & x: mp) {
        ans = max(ans, x.second.first / x.second.second);
    }
    return ans;
}
```

# MY code

```python
class Solution:
    # @param A : list of list of strings
    # @return an integer
    def highestScore(self, A):
        A = sorted(A, key=lambda x: x[0])
        d = len(A)
        s = A[0][0]
        ans = int(A[0][1])
        answ = 0
        count = 1
        i = 1
        if d==1:
            return int(A[0][1])
        while(i < d):
            if s == A[i][0]:
                ans += int(A[i][1])
                count += 1
                
            else:
                answ = max(ans//count, answ)
                count = 1
                ans = int(A[i][1])
            s = A[i][0]
            i+=1
        
        answ  = max(answ, ans//count)
        return int(answ)
```