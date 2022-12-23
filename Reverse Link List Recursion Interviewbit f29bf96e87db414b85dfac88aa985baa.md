# Reverse Link List Recursion | Interviewbit

Created: July 12, 2022 8:09 PM
Tags: Linked List
URL: https://www.interviewbit.com/problems/reverse-link-list-recursion/

Reverse a linked list using recursion.

**Example :**
 Given `1->2->3->4->5->NULL`,

return `5->4->3->2->1->NULL`.

**PROBLEM APPROACH :**

Complete solution code in the hints

Note:You only need to implement the given function. Do not read input, instead use the arguments to the function. Do not print the output, instead return values as specified. Still have a question? Checkout [Sample Codes](https://www.interviewbit.com/pages/sample_codes/) for more details.

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
ListNode* Solution::reverseList(ListNode* A) {
    // smallest linked list
    if(A->next == NULL or A == NULL){
        return A;
    }
    
    // recursive case make a call on smaller part
    ListNode* shead = reverseList(A->next);
    A->next->next= A;;
    A ->next = NULL;
    return shead;
}
```