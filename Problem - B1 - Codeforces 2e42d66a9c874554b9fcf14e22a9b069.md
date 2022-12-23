# Problem - B1 - Codeforces

Created: May 9, 2022 2:04 AM
URL: https://codeforces.com/contest/1678/problem/B1

![codeforces-telegram-square.png](Problem%20-%20B1%20-%20Codeforces%202e42d66a9c874554b9fcf14e22a9b069/codeforces-telegram-square.png)

This is the easy version of the problem. The only difference between the two versions is that the harder version asks additionally for a minimum number of subsegments.

Now Tokitsukaze divides  into the minimum number of contiguous subsegments, and for each subsegment, all bits in each subsegment are the same. After that,  is considered good if the lengths of all subsegments are even.

For example, if  is "11001111", it will be divided into "11", "00" and "1111". Their lengths are , ,  respectively, which are all even numbers, so "11001111" is good. Another example, if  is "1110011000", it will be divided into "111", "00", "11" and "000", and their lengths are , , , . Obviously, "1110011000" is not good.

Tokitsukaze wants to make  good by changing the values of some positions in . Specifically, she can perform the operation any number of times: change the value of  to '0' or '1'(). Can you tell her the minimum number of operations to make  good?

For each test case, the first line contains a single integer  () — the length of , it is guaranteed that  is even.

Change ,  and  to '0', after that  becomes "1100000000", it can be divided into "11" and "00000000", which lengths are  and  respectively. There are other ways to operate  times to make  good, such as "1111110000", "1100001100", "1111001100".

In the second, third and fourth test cases,  is good initially, so no operation is required.

```cpp
for _ in range(int(input())):
    n = int(input())
    s = input()
    count = 0
    ans = 0
    while(count<n-1):
        if s[count]!=s[count+1]:
            ans += 1
        count += 2
    print(ans)
```