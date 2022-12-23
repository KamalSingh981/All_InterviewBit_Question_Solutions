# Next Smallest Palindrome! | Interviewbit

Created: May 19, 2022 11:10 PM
URL: https://www.interviewbit.com/problems/next-smallest-palindrome/

**Problem Description**

Given a numeric string **A** representing a large number you need to find the **next smallest palindrome** greater than this number.

**Problem Constraints**

1 <= |A| <= 100

A doesn't start with zeroes and always contain digits from 0-9.

**Input Format**

First and only argument is an string **A**.

**Output Format**

Return a numeric string denoting the **next smallest palindrome** greater than A.

**Example Input**

Input 1:

```
 A = "23545"

```

Input 2:

```
 A = "999"

```

**Example Output**

```python
class Solution:
    # @param A : string
    # @return a strings
    def is_palindrome(self, a):
        return a == a[::-1]

    def compare(self, x, y):
        for i, j in zip(x, y):
            if i > j: return 1
            elif j > i: return -1
            else: continue
        return 0

    def add_1(self, a):
        ns = ""
        carry = 1
        for c in reversed(a):
            d, r = divmod(int(c) + carry, 10)
            ns += str(r)
            carry = d
        if carry: ns += str(carry)

        return ns[::-1]

    def handle_odd(self, a):
        n = len(a)
        mid = n//2
        left = a[:mid]
        right = a[mid+1:]
        if self.compare(left[::-1], right) == 1:
            return left + a[mid] + left[::-1]
        else:
            left = left + a[mid]
            left = self.add_1(left)
            return left + left[::-1][1:]

    def handle_even(self, a):
        n = len(a)
        left = a[:n//2]
        right = a[n//2:]
        if self.compare(left[::-1], right) == 1:
            return left + left[::-1]
        else:
            left = self.add_1(left)
            return left + left[::-1]

    def solve(self, A):
        if self.is_palindrome(A): A = self.add_1(A)
        if self.is_palindrome(A): return A 

        n = len(A)
        if n & 1:
            return self.handle_odd(A)
        else:
            return self.handle_even(A)
```

```cpp
string Solution::solve(string A) {
    int size = A.size();
    int mid = (size+1)/2;

    bool incr = true;
    // check if we need to add 1 to first half of the number
    // before making it into a palindrome.
    for(int i = mid; i < size; i++) {
        if(A[size-1-i] == A[i]) continue;
        if(A[size-1-i] < A[i]) incr = true;
        if(A[size-1-i] > A[i]) incr = false;
        break;
    }

    A = A.substr(0,mid);

    //add 1 to the first half of the number.
    if(incr) {
        int carry = 1;

        for(int i = mid-1; i >= 0 && carry == 1; i--)
            A[i] = ( A[i] == '9' ? '0' : A[i] + carry--);

        if(carry) //every digit must have been '9'
            return '1' + string(size-1,'0') + '1';
    }

    //append the first half reversed to make the palindrome.
    for(int i = size-A.size()-1; i >= 0; i--)
        A.push_back(A[i]);

    return A;
}
```

Algorithm

Divide it into three conditions palindrome, odd and even

odd case:

97531 —→ 97579

copy the left to  the right, keep the middle

23545 ——→ 23532

23532 ——→ 23632 

copy the left to the right 

if(reversed(left) <right: keep mid)

else: mid + 1

even case:

1337 ——→ 1331 ———> 1441

if reversed(left) > right: 

else: left +1

copy the left to the right 

8999 ——> 9009

Palindrome case

99 —→ 101

1337 ——→ 1441