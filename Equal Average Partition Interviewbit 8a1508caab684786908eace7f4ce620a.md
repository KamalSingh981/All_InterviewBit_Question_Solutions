# Equal Average Partition | Interviewbit

Created: August 7, 2022 11:18 PM
Tags: Dynamic Programming
URL: https://www.interviewbit.com/problems/equal-average-partition/

**Problem Description**

Given an array **A** with non negative numbers, divide the array into two parts such that the average of both the parts is equal.

Return both parts (If exist). If there is no solution. return an empty list.

**NOTE:**

If a solution exists, you should return a list of exactly 2 lists of integers A and B which follow the following condition :

- numElements in A <= numElements in B
- If numElements in A = numElements in B, then A is lexicographically smaller than B ( https://en.wikipedia.org/wiki/Lexicographical_order )

If multiple solutions exist, return the solution where length(A) is minimum. If there is still a tie, return the one where A is lexicographically smallest.

Array will contain only non negative numbers.

- *Input Format**

First andonly argument is an integer array **A**.

- *Output Format**

Return 2D array consisting of two rows where each row denoted a partition.

- *Example Input**

**Example Output**

**Example Explanation**

Explanation 1:

```
 The average of part is (15+9)/2 = 12, average of second part elements is (1 + 7 + 11 + 29) / 4 = 12

```

```cpp
bool isPossible(int i, int sum, int n, vector<int> &A, vector<vector<vector<bool>>> &dp, vector<int> &a){
    if(n == 0) return sum == 0;
    if(i>= A.size()) return false;
    
    if(dp[i][sum][n] == false) return false;
    
    if(A[i] <= sum){
        a.push_back(A[i]);
        if(isPossible(i+1, sum - A[i], n -1, A, dp, a)){
            return dp[i][sum][n] = true;
        }
        a.pop_back();
    }
    
    if(isPossible(i+1, sum, n, A, dp, a)){
        return dp[i][sum][n] = true;
    }
    
    return dp[i][sum][n] = false; 
}

vector<vector<int> > Solution::avgset(vector<int> &A) {
    int n = A.size();
    sort(A.begin(), A.end());
    
    int sum = 0;
    for(auto it:A){
        sum += it;
    }
    
    vector<vector<vector<bool>>> t(n, vector<vector<bool>>(sum + 1, vector<bool>(n, true)));
    vector<int> parta;
    for(int i = 1; i<n; i++){
        if((sum*i)%n == 0){
            int s = (sum*i)/n;
            vector<int> a;
            
            if(isPossible(0, s, i, A, t, a)){
                sort(a.begin(), a.end());
                parta = a;
                break;
            }
            
        }
    }
    
    vector<vector<int>> ans;
    vector<int> partb;
    if(parta.size() == 0) return ans;
    int i = 0, j = 0;
    
    while(i<n){
        if(j<parta.size() and parta[j] == A[i]){
            i++;
            j++;
        }
        else{
            partb.push_back(A[i]);
            i++;
        }
    }
    
    ans.push_back(parta);
    ans.push_back(partb);
    return ans;   
}
```