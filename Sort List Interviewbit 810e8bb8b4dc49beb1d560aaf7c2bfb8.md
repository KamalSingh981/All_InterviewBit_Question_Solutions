# Sort List | Interviewbit

Created: June 21, 2022 2:20 PM
Tags: Linked List
URL: https://www.interviewbit.com/problems/sort-list/

Sort a linked list in `O(n log n)` time using constant space complexity.

**Example :**

```
Input : 1 -> 5 -> 4 -> 3

Returned list : 1 -> 3 -> 4 -> 5

```

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
 
 ListNode* midpoint(ListNode* head){
     if(head == NULL || head->next == NULL){
         return head;
     }
     
     ListNode* slow = head;
     ListNode* fast = head->next;
     while(fast!=NULL and fast->next != NULL){
         slow = slow->next;
         fast = fast->next->next;
     }
     return slow;   
 }
 
 ListNode* merge(ListNode*a, ListNode*b){
     if(a==NULL){
         return b;
     }
     if(b == NULL){
         return a;
     }
     
     ListNode*c;
     if(a->val > b->val){
         c = b;
         c->next = merge(a, b->next);
     }
     else{
         c = a;
         c->next = merge(a->next, b);
     }
     
     return c;
 }
 
 ListNode* mergesort(ListNode* a){
     if(a == NULL || a->next == NULL){
         return a;
     }
     
     ListNode* mid = midpoint(a);
     ListNode*c = a;
     ListNode*d = mid->next;
     mid->next = NULL;
     
     c = mergesort(c);
     d = mergesort(d);
     ListNode* e = merge(c,d);
     return e;
 }
 
 
ListNode* Solution::sortList(ListNode* A) {
    return mergesort(A);
}e
```