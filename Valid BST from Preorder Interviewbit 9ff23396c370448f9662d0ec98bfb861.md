# Valid BST from Preorder | Interviewbit

Created: July 22, 2022 4:36 PM
Tags: Graphs
URL: https://www.interviewbit.com/problems/valid-bst-from-preorder/

**Problem Description**

You are given a preorder traversal **A**, of a Binary Search Tree.

Find if it is a valid preorder traversal of a BST.

**Note:** Binary Search Tree by definition has distinct keys and **duplicates in binary search tree are not allowed**.

**Problem Constraints**

1 <= A[i] <= 106

1 <= |A| <= 105

**Input Format**

First and only argument is an integer array **A** denoting the pre-order traversal.

**Output Format**

Return an integer:

- 0 : Impossible preorder traversal of a BST
- 1 : Possible preorder traversal of a BST

**Example Input**

Input 1:

```
A = [7, 7, 10, 10, 9, 5, 2, 8]

```

**Example Output**

![Valid%20BST%20from%20Preorder%20Interviewbit%209ff23396c370448f9662d0ec98bfb861/superman.e804d3.png](Valid%20BST%20from%20Preorder%20Interviewbit%209ff23396c370448f9662d0ec98bfb861/superman.e804d3.png)

```cpp
int Solution::solve(vector<int> &A) {
    unordered_map<int, int> m;
    for(auto i:A){
        if(m.find(i) != m.end()){
            return false;

        }
        m[i];
    }
    stack<int> s;
    int root= INT_MIN;
    for(int i= 0; i<A.size(); i++){
        while(!s.empty() and A[i] > s.top()){
            root = s.top();
            s.pop();
        }
        
        if(A[i] < root){
            return false;
        }
        s.push(A[i]);
    }
    return true;
}
```