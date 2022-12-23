# Merge Two Sorted Lists | Interviewbit

Created: June 21, 2022 2:24 PM
Tags: Linked List
URL: https://www.interviewbit.com/problems/merge-two-sorted-lists/

Merge two sorted linked lists and return it as a new list. 
 The new list should be made by splicing together the nodes of the first two lists, and should also be sorted.

For example, given following linked lists :

```
  5 -> 8 -> 20
  4 -> 11 -> 15

```

The merged list should be :

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
ListNode* Solution::mergeTwoLists(ListNode* A, ListNode* B) {
    if(A==NULL){
        return B;
    }
    if(B==NULL){
        return A;
    }
    
    if(A->val < B->val){
        A->next = mergeTwoLists(A->next, B);
    }
    else{
        B->next = mergeTwoLists(A, B->next);
        A = B;
    }
    return A;
}
```

## Without Using Recursion

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
ListNode* Solution::mergeTwoLists(ListNode* A, ListNode* B) {
    ListNode *ret, *temp, *rettemp;
    if (!A) {
        return B;
    }
    if (!B) {
        return A;
    }
    if (A->val <= B->val) {
        ret = new ListNode(A->val);
        A = A->next;
    } else {
        ret = new ListNode(B->val);
        B = B->next;
    }
    
    temp = ret;
    while (A&&B) {
        if (A->val <= B->val) {
            temp->next = new ListNode(A->val);
            A = A->next;
        } else {
            temp->next = new ListNode(B->val);
            B = B->next;
        }
        temp = temp->next;
    }
    while (A) {
        temp->next = new ListNode(A->val);
        A = A->next;
        temp = temp->next;
    }
    while (B) {
        temp->next = new ListNode(B->val);
        B = B->next;
        temp = temp->next;
    }
    
    return ret;
}
```