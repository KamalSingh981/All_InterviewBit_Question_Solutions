# Maximum Consecutive Gap | Interviewbit

Created: May 16, 2022 12:48 AM
URL: https://www.interviewbit.com/problems/maximum-consecutive-gap/

Given an unsorted array, find the maximum difference between the successive elements in its sorted form.

Try to solve it in linear time/space.

**Example :**

**Return 0 if the array contains less than 2 elements.**

- You may assume that all the elements in the array are non-negative integers and fit in the 32-bit signed integer range.
- You may also assume that the difference will not overflow.

```python
int Solution::maximumGap(const vector<int> &num) {
    if(num.empty() || num.size() < 2)
        return 0;
    int maxNum = *max_element(num.begin(), num.end());
    int minNum = *min_element(num.begin(), num.end());
    //average gap from minNum to maxNum.
    int gap = (maxNum - minNum - 1) / (num.size() - 1) + 1;

    //number of buckets = num.size() - 1
    vector<int> bucketsMin(num.size() - 1, INT_MAX);
    vector<int> bucketsMax(num.size() - 1, INT_MIN);
    //put into buckets
    for (int i = 0; i < num.size(); i++) {
        if (num[i] != maxNum && num[i] != minNum)
        {
            int buckInd = (num[i] - minNum) / gap;
            bucketsMin[buckInd] = min(bucketsMin[buckInd], num[i]);
            bucketsMax[buckInd] = max(bucketsMax[buckInd], num[i]);
        }
    }
    int maxGap = INT_MIN;
    int previous = minNum;
    for (int i = 0; i < num.size() - 1; i++) {
        if (bucketsMin[i] == INT_MAX && bucketsMax[i] == INT_MIN)
            continue;   //empty
        //i_th gap is minvalue in i+1_th bucket minus maxvalue in i_th bucket 
        maxGap = max(maxGap, bucketsMin[i] - previous);
        previous = bucketsMax[i];
    }
    maxGap = max(maxGap, maxNum - previous);
    return maxGap;
}
```

Algorithm

Now, first try to think if you were already given the minimum value `MIN` and maximum value `MAX` in the array of size `N`, under what circumstances would the max gap be minimum and maximum ?

Obviously, maximum gap will be maximum when all elements are either `MIN` or `MAX` making maxgap = `MAX` - `MIN`.

Maximum gap will be minimum when all the elements are equally spaced apart between `MIN` and `MAX`. Lets say the spacing between them is gap.

So, they are arranged as

`MIN, MIN + gap, MIN + 2*gap, MIN + 3*gap, ... MIN + (N-1)*gap`

where

`MIN + (N-1)*gap = MAX 
=> gap = (MAX - MIN) / (N - 1).`

So, we know now that our answer will lie in the range `[gap, MAX - MIN]`.Now, if we know the answer is more than gap, what we do is create buckets of size gap for ranges

  `[MIN, MIN + gap), [Min + gap, `MIN` + 2* gap) ... and so on`

There will only be `(N-1)` such buckets. We place the numbers in these buckets based on their value.

If you pick any 2 numbers from a single bucket, their difference will be less than gap, and hence they would never contribute to `maxgap` ( Remember `maxgap` >= `gap` ). We only need to store the largest number and the smallest number in each bucket, and we only look at the numbers across bucket.

Now, we just need to go through the bucket sequentially ( they are already sorted by value ), and get the difference of min_value with max_value of previous bucket with at least one value. We take maximum of all such values.