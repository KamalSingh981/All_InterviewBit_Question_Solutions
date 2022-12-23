# Remove Duplicates from Sorted List | Interviewbit

Created: June 21, 2022 1:42 PM
Tags: Linked List
URL: https://www.interviewbit.com/problems/remove-duplicates-from-sorted-list/

Given a sorted linked list, delete all duplicates such that each element appear only once.

For example,
 Given `1->1->2`, return `1->2`.
 Given `1->1->2->3->3`, return `1->2->3`.

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
 void deleteNode(ListNode*&A){
     ListNode* temp = A->next;
     A->next = A->next->next;
     delete temp;
 }
 
ListNode* Solution::deleteDuplicates(ListNode* A) {
    ListNode* a = A;
    while(A->next!=NULL){
        if(A->val == A->next->val){
            deleteNode(A);
        }
        else{
            A = A->next;
        }
    }
    return a;
}
```