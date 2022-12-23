# List Cycle | Interviewbit

Created: June 21, 2022 3:02 PM
Tags: Linked List
URL: https://www.interviewbit.com/problems/list-cycle/

Given a linked list, return the node where the cycle begins. If there is no cycle, return null.

Try solving it using constant additional space.

**Example:**

```
Input:

              ______
             |     |
             \/    |
    1 -> 2 -> 3 -> 4
Return the node corresponding to node 3.

```

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */

ListNode* Solution::detectCycle(ListNode* A) {
    // Do not write main() function.
    // Do not read input, instead use the arguments to the function.
    // Do not print the output, instead return values as specified
    // Still have a doubt. Checkout www.interviewbit.com/pages/sample_codes/ for more details
    
    ListNode* slow = A;
    ListNode* fast = A;
    
    while(fast != NULL and fast->next != NULL){
        fast = fast->next->next;
        slow = slow->next;
        if(fast == slow){
            slow = A;
            while(fast != slow){
                slow = slow->next;
                fast = fast->next;
            }
            return fast;
        }
    }
    return NULL;
}
```