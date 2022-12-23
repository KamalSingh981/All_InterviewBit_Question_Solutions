# Maximum Sum Combinations | Interviewbit

Created: July 18, 2022 5:59 PM
Tags: Heap
URL: https://www.interviewbit.com/problems/maximum-sum-combinations/

**Problem Description**

Given two equally sized 1-D arrays **A, B** containing **N** integers each.

A **sum combination** is made by adding one element from array **A** and another element of array **B**.

Return the **maximum C valid sum combinations** from all the possible sum combinations.

**Problem Constraints**

1 <= N <= 105

1 <= A[i] <= 103

1 <= C <= N

**Input Format**

First argument is an one-dimensional integer array **A** of size **N**.

Second argument is an one-dimensional integer array **B** of size **N**.

Third argument is an integer **C**.

**Output Format**

Return a one-dimensional integer array of size **C** denoting the top C maximum sum combinations.

**NOTE:**

The returned array must be sorted in non-increasing order.

**Example Input**

Input 1:

```
 A = [3, 2]
 B = [1, 4]
 C = 2

```

Input 2:

```
 A = [1, 4, 2, 3]
 B = [2, 5, 1, 6]
 C = 4

```

**Example Output**

Output 1:

```
 [7, 6]

```

Output 1:

```
 [10, 9, 9, 8]

```

**Example Explanation**

Explanation 1:

```
 7     (A : 3) + (B : 4)
 6     (A : 2) + (B : 4)

```

Explanation 2:

```
 10   (A : 4) + (B : 6)
 9   (A : 4) + (B : 5)
 9   (A : 3) + (B : 6)
 8   (A : 3) + (B : 5)

```

```cpp
class three{
    public:
    int val, idx, jdx;
};
struct comp{
    bool operator()(three a, three b){
        return a.val<b.val;
    }
};

vector<int> Solution::solve(vector<int> &A, vector<int> &B, int C) {
    
   sort(A.begin(), A.end());
   sort(B.begin(), B.end());
   
   priority_queue<three, vector<three>, comp> pq;
   
   set<pair<int, int>> s;
   
   vector<int> ans;
   
   int n = A.size();
   
   pq.push({A[n-1] + B[n-1], n-1, n-1});
   s.insert({n -1, n -1});
   
   
   while(ans.size() != C){
       three th = pq.top(); pq.pop();
       int vl = th.val, i= th.idx, j = th.jdx;
       ans.push_back(vl);
       
       if(i>0 and s.count({i-1, j})==0){
           pq.push({A[i-1] + B[j], i-1, j});
           s.insert({i -1 , j});
       }
       
       if(j > 0 and s.count({i, j-1})==0){
           pq.push({A[i] + B[j-1], i, j-1});
           s.insert({i , j-1});

       }
   }
    return ans;
}
```

Interview Bit Code

```cpp
vector<int> KMaxCombinations(vector<int>& A,vector<int>& B, int K)
{
    // sort both arrays A and B
    sort(A.begin(), A.end());
    sort(B.begin(), B.end());
    vector<int>ans;
    int N = A.size();

    // Max heap which contains tuple of the format
    // (sum, (i, j)) i and j are the indices
    // of the elements from array A
    // and array B which make up the sum.
    priority_queue<pair<int, pair<int, int> > > pq;

    // my_set is used to store the indices of
    // the  pair(i, j) we use my_set to make sure
    // the indices doe not repeat inside max heap.
    set<pair<int, int> > my_set;

    // initialize the heap with the maximum sum
    // combination ie (A[N - 1] + B[N - 1])
    // and also push indices (N - 1, N - 1) along
    // with sum.
    pq.push(make_pair(A[N - 1] + B[N - 1],
                      make_pair(N-1, N-1)));

    my_set.insert(make_pair(N - 1, N - 1));

    // iterate upto K
    for (int count=0; count<K; count++) {

        // tuple format (sum, (i, j)).
        pair<int, pair<int, int> > temp = pq.top();
        pq.pop();

        ans.push_back(temp.first);

        int i = temp.second.first;
        int j = temp.second.second;

        if(i-1>=0)
        {
            int sum = A[i - 1] + B[j];

        // insert (A[i - 1] + B[j], (i - 1, j))
        // into max heap.
        pair<int, int> temp1 = make_pair(i - 1, j);

        // insert only if the pair (i - 1, j) is
        // not already present inside the map i.e.
        // no repeating pair should be present inside
        // the heap.
        if (my_set.find(temp1) == my_set.end()) {
            pq.push(make_pair(sum, temp1));
            my_set.insert(temp1);
        }
        }

        // insert (A[i] + B[j - 1], (i, j - 1))
        // into max heap
        if(j-1>=0)
        {
        int sum = A[i] + B[j - 1];
        pair<int,int>temp1 = make_pair(i, j - 1);

        // insert only if the pair (i, j - 1)
        // is not present inside the heap.
        if (my_set.find(temp1) == my_set.end()) {
            pq.push(make_pair(sum, temp1));
            my_set.insert(temp1);
        }
        }
    }
    return ans;
}
vector<int> Solution::solve(vector<int> &A, vector<int> &B, int C) {
    vector<int>temp=KMaxCombinations(A,B,C);
    return temp;
}
```