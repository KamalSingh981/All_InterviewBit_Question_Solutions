# Bulbs | Interviewbit

Created: July 24, 2022 10:38 PM
Tags: GreedyAlgorithm
URL: https://www.interviewbit.com/problems/interview-questions/

**Problem Description**

**N** light bulbs are connected by a wire.

Each bulb has a switch associated with it, however due to faulty wiring, a switch also changes the state of all the bulbs to the right of current bulb.

Given an initial state of all bulbs, find the minimum number of switches you have to press to turn on all the bulbs.

You can press the same switch multiple times.

**Note** : 0 represents the bulb is off and 1 represents the bulb is on.

**Problem Constraints**

**Input Format**

The first and the only argument contains an integer array A, of size N.

**Output Format**

**Example Input**

**Example Output**

**Example Explanation**

press switch 0 : [1 0 1 0]
 press switch 1 : [1 1 0 1]
 press switch 2 : [1 1 1 0]
 press switch 3 : [1 1 1 1]

Note:You only need to implement the given function. Do not read input, instead use the arguments to the function. Do not print the output, instead return values as specified. Still have a question? Checkout [Sample Codes](https://www.interviewbit.com/pages/sample_codes/) for more details.

```cpp
int Solution::bulbs(vector<int> &A) {
    int ans = 0;
    int l = 0;
    for(auto i: A){
        if( l == 0 and i == 0){
            ans++;
            l = 1;
        }
        else if(l == 1 and i == 1){
            ans++;
            l = 0;
        }
    }
    return ans;  
}
```