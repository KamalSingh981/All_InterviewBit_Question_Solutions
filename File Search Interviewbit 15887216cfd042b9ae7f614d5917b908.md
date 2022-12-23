# File Search | Interviewbit

Created: July 27, 2022 11:09 PM
Tags: DFS, Graphs
URL: https://www.interviewbit.com/problems/file-search/

**Problem Description**

You are given an assignment to sort out the files of your department today.
 A file contains various records. Each record has an (ID, Parent ID).
 To make your task easier, you decided to separate records into different sets.
 If a set contains a record with (ID, Parent ID) - (X, Y), then both X and Y must be present in the set.
 There are **A** records. You are also given a 2D array **B** of dimensions **N x 2**,
 where each row is record's (ID, Parent ID).

You have to find the maximum number of sets you can divide the records into.

**Problem Constraints**

1 <= A, N <= 105
 1 <= B[i][0], B[i][1] <= A
 There can be duplicate records.
 There can be two records (X, Y) and (Y, X).

**Input Format**

The first argument is the integer A.
 The second argument is the 2D integer array B.

**Output Format**

**Example Input**

Input 1:

```
A = 4
B = [[1, 2], [3, 4]]

```

Input 2:

```
A = 4
B = [[1, 2], [3, 4], [2, 4]]

```

**Example Output**

Output 1:

```
2

```

Output 2:

```
1

```

**Example Explanation**

Explanation 1:

```
We can create two sets (1, 2), (3, 4). Since, (1, 2) need to be together and (3, 4).
```

Explanation 2:

```
We can only have 1 set because (1, 2) need to be together (2, 4) need to be together.
Hence, (1, 2, 4) need to be together. Similarly, (1, 2, 3, 4) need to be together. Therefore, the answer is 1.

```

Note:You only need to implement the given function. Do not read input, instead use the arguments to the function. Do not print the output, instead return values as specified. Still have a question? Checkout [Sample Codes](https://www.interviewbit.com/pages/sample_codes/) for more details.

```cpp

```