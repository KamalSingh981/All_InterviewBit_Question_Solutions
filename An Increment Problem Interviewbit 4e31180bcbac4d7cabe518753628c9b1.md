# An Increment Problem | Interviewbit

Created: July 15, 2022 12:23 PM
Tags: Hashing
URL: https://www.interviewbit.com/problems/an-increment-problem/

**Problem Description**

Given a stream of numbers **A**. On arrival of each number, you need to increase its first occurence by 1 and include this in the stream.

Return the final stream of numbers.

**Problem Constraints**

1 <= |A| <= 100000

1 <= A[i] <= 10000

**Input Format**

First and only argument is the array A.

**Output Format**

Return an array, the final stream of numbers.

**Example Input**

Input 1:

```
A = [1, 1]

```

Input 2:

```
A = [1, 2]

```

**Example Output**

Output 1:

```
[2, 1]

```

Output 2:

```
[1, 2]

```

**Example Explanation**

Explanation 1:

```
 On arrival of the second element, the other element is increased by 1.

```

Explanation 2:

```
No increases are to be done.

```

```cpp
vector<int> Solution::solve(vector<int> &A) {

   unordered_map<int,int> m;

   for( int i = 0 ; i < A.size() ; i++ ){
       if(m.find(A[i]) == m.end()){
           m[A[i]] = i;  // If the element is not present in the hashmap
       }
       else{          
           int index = m[A[i]];
           A[index]++;
           if(m.find(A[index]) == m.end()){
               // If new element is not present in the hashmap then simply add in
               m[A[index]] = index;
           }
           else{
               if(m[A[index]]>index){
                   m[A[index]] = index;
               }
           }          
           m[A[i]] = i;
       }
   }
   return A;
}
```

Algorithm

We will use a unordered map for this question. Key will be the element and value be the index of that element. if the element if occurring for the first time we will simply add it to the HashMap. Else we will take the index of first occurrence of that element and increate that element by 1. After this we will check whether the new element formed is in the HashMap is present or not. If it is not then add it to then map with then index else,  we will check that the index of first occurrence of that element is smaller then the currently formed element if not then update it. At last update the index  of current element in the map.