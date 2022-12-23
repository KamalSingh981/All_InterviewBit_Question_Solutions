# Gas Station | Interviewbit

Created: July 10, 2022 12:41 AM
Tags: GreedyAlgorithm
URL: https://www.interviewbit.com/problems/gas-station/

**Problem Description**

Given two integer arrays **A** and **B** of size **N**. There are **N** gas stations along a circular route, where the amount of gas at station **i** is **A[i]**.

You have a car with an unlimited gas tank and it costs **B[i]** of gas to travel from station **i** to its next station **(i+1)**. You begin the journey with an empty tank at one of the gas stations.

Return the minimum starting gas station's index if you can travel around the circuit once, otherwise return **-1**.

You can only travel in one direction. i to **i+1, i+2, ... n-1, 0, 1, 2..** Completing the circuit means starting at i and ending up at i again.

**Input Format**

The first argument given is the integer array A. The second argument given is the integer array B.

**Output Format**

Return the minimum starting gas station's index if you can travel around the circuit once, otherwise return -1.

**Example Input**

**Example Output**

**Example Explanation**

If you start from index 0, you can fill in A[0] = 1 amount of gas. Now your tank has 1 unit of gas. But you need B[0] = 2 gas to travel to station 1. If you start from index 1, you can fill in A[1] = 2 amount of gas. Now your tank has 2 units of gas. You need B[1] = 1 gas to get to station 0. So, you travel to station 0 and still have 1 unit of gas left over. You fill in A[0] = 1 unit of additional gas, making your current gas = 2. It costs you B[0] = 2 to get to station 1, which you do and complete the circuit.

```cpp
int Solution::canCompleteCircuit(const vector<int> &A, const vector<int> &B) {
    int tank =0, total = 0, index = 0;
    for(int i=0; i<A.size(); i++){
        int consume = A[i] - B[i];
        tank += consume;
        if(tank<0){
            index = i +1;
            tank = 0;
        }  
        total += consume;   
    }
    
    if(total < 0){
        return -1;
    }
    else{
        return index;
    }
}
```

O(N^2)

```cpp
bool check(int i, vector<int> A, vector<int> B){
    int gas_amount = 0;
    int n = A.size();
    int index = 0;
    for(int j = 0; j<n; j++){
        index = (i+j)%n;
        gas_amount += A[index] - B[index];
        if(gas_amount<0){
            return false;
        }
    } 
    return true;   
}

int Solution::canCompleteCircuit(const vector<int> &A, const vector<int> &B) {
    for(int i=0; i<A.size(); i++){
        if(check(i, A, B)){
            return i;
        }
    }
    
    return -1;
```