# Find Duplicate in Array | Interviewbit

Created: May 11, 2022 10:17 PM
URL: https://www.interviewbit.com/problems/find-duplicate-in-array/

Given a read only array of n + 1 integers between 1 and n, find one number that repeats in linear time using less than O(n) space and traversing the stream sequentially O(1) times.

**Sample Input:** 
`[3 4 1 4 1]`
 **Sample Output:** 
`1`
 If there are multiple possible answers ( like in the sample case above ), output any one.

If there is no duplicate, output -1

```cpp
int Solution::repeatedNumber(const vector<int> &A) {
    int s = A.size()-1;
    int sq = sqrt(s);
    int range = s/sq + 1;
    int count[range] = {0};
    for(int i=0; i<=s; i++){
        count[(A[i] - 1)/sq]++;
    }
    int selblock = range - 1;
    for(int i=0; i<range-1; i++){
        if(count[i]>sq){
            selblock = i;
            break;
        }
    }

    unordered_map<int, int> m;
    for(int i =0; i<= s; i++){
            if(((selblock*sq)<A[i]) && (A[i] <= ((selblock+1)*sq))){
                m[A[i]]++;
                if(m[A[i]]>1){
                    return A[i];
                }
            }
    }

    return -1;
}
```