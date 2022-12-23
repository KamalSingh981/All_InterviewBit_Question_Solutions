# Hotel Bookings Possible | Interviewbit

Created: May 15, 2022 2:21 AM
URL: https://www.interviewbit.com/problems/hotel-bookings-possible/

**Problem Description**

A hotel manager has to process **N** advance bookings of rooms for the next season. His hotel has **C** rooms. Bookings contain an arrival date and a departure date. He wants to find out whether there are enough rooms in the hotel to satisfy the demand. Write a program that solves this problem in time O(N log N) .

**Input Format**

First argument is an integer array A containing arrival time of booking.
 Second argument is an integer array B containing departure time of booking.
 Third argument is an integer C denoting the count of rooms.

**Output Format**

Return True if there are enough rooms for N bookings else return False.
 Return 0/1 for C programs.

**Example Input**

**Example Output**

**Example Explanation**

Explanation 1:

```
 At day = 5, there are 2 guests in the hotel. But I have only one room.
```

```cpp
bool areBookingsPossible(vector<int> A, vector<int> B,
                           int K, int N)
{
    sort(A.begin(), A.end());
    sort(B.begin(), B .end());
     
    for(int i = 0; i < N; i++)
    {
        if (i + K < N && A[i + K] < B[i])
        {
            return false;
        }
    }
    return true;
}
bool Solution::hotel(vector<int> &arrive, vector<int> &depart, int K) {
    int n = arrive.size();
    return areBookingsPossible(arrive, depart, K, n);
}
```