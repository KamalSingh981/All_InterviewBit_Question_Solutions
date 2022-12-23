# WoodCutting Made Easy! | Interviewbit

Created: May 25, 2022 11:45 AM
Tags: bit manipullation
URL: https://www.interviewbit.com/problems/woodcutting-made-easy/

**Problem Description**

There is given an integer array **A** of size **N** denoting the heights of **N** trees.

Lumberjack Ojas needs to chop down **B** metres of wood. It is an easy job for him since he has a nifty new woodcutting machine that can take down forests like wildfire. However, Ojas is only allowed to cut a single row of trees.

Ojas's machine works as follows: Ojas sets a height parameter **H** (in metres), and the machine raises a giant sawblade to that height and cuts off all tree parts higher than **H** (of course, trees not higher than **H** meters remain intact). Ojas then takes the parts that were cut off. For example, if the tree row contains trees with heights of 20, 15, 10, and 17 metres, and Ojas raises his sawblade to 15 metres, the remaining tree heights after cutting will be 15, 15, 10, and 15 metres, respectively, while Ojas will take 5 metres off the first tree and 2 metres off the fourth tree (7 metres of wood in total).

Ojas is **ecologically** minded, so he doesn't want to cut off more wood than necessary. That's why he wants to set his sawblade as high as possible. Help Ojas find the **maximum integer height** of the sawblade that still allows him to cut off **at least B** metres of wood.

**NOTE:**

- The sum of all heights will exceed **B**, thus Ojas will always be able to obtain the required amount of wood.

**Problem Constraints***Input Format*

*First argument is an integer array **A** of size **N** denoting the heights of each tree(in metres).*

*Second argument is an integer **B**.*

*Output Format*

*Return a single integer denoting **maximum integer height** of the sawblade that still allows him to cut off **at least B** metres of wood.*

*Example Input*

*Input 1: 

 `A = [20, 15, 10, 17]
 B = 7`
 
Input 2: 

 `A = [4, 42, 40, 26, 46]
 B = 20`*

*Example Output*

*Example Explanation*

- 

Explanation 1:

```
 If you the height parameter to 15 then you can chop:
  5 metres from first tree
  0 metres from second tree
  0 metres from third tree
  2 metres from fourth tree
  So in total you chopped 7 metres of wood.

```

Explanation 2:

```
 If you the height parameter to 36 then you can chop:
  0 metres from first tree
  6 metres from second tree
  4 metres from third tree
  0 metres from fourth tree
  10 metres from fifth tree
  So in total you chopped 20 metres of wood.

```

```cpp
long long findsum(vector<int> A, int B){
    long long sum = 0;
    for(int i=0; i<A.size(); i++){
        if(A[i]>B){
            sum += A[i] - B;
        }
    }
    return sum;
}

int Solution::solve(vector<int> &A, int B) {
    int h = *max_element(A.begin(), A.end());
    int l = 0;
    int mid;
    while(l<h){
        mid = (l + h)/2;
        long long sum = findsum(A, mid);
        if(sum == B || l == mid){
            return mid;
        }
        else if(sum>B){
            l = mid;
        }
        else{
            h = mid;
        }
    }
    return mid;
}
```