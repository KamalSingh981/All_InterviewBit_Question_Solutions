# Reverse Link List II | Interviewbit

Created: June 21, 2022 12:38 PM
Tags: Linked List
URL: https://www.interviewbit.com/problems/reverse-link-list-ii/

Reverse a linked list from position m to n. Do it in-place and in one-pass.

For example:
 Given `1->2->3->4->5->NULL`, `m = 2` and `n = 4`,

return `1->4->3->2->5->NULL`.

> 
> 
> 
> **Note:** Given m, n satisfy the following condition: `1 ≤ m ≤ n ≤ length of list`.
> 
> **Note 2:** Usually the version often seen in the interviews is reversing the whole linked list which is obviously an easier version of this question.
> 

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
ListNode* Solution::reverseBetween(ListNode* A, int B, int C) {
    ListNode* n = new ListNode(0);
    n->next = A;
    A = n;
    ListNode* temp = A;
    while(temp){
        if(B==1){
            ListNode* prev = NULL, *fur = temp->next, *curr= temp->next,*before =temp->next;
            while(C){
                fur = fur->next;
                curr->next = prev;
                prev = curr;
                curr = fur;
                C--;
            }
            before->next = fur;
            temp->next = prev;
            
        }
        temp = temp ->next;
        B--;
        C--;
    }
    
    
    return A->next;    
}
```