# Rotate List | Interviewbit

Created: June 22, 2022 2:00 AM
Tags: Linked List
URL: https://www.interviewbit.com/problems/rotate-list/

Given a list, rotate the list to the right by k places, where k is non-negative.

For example:

Given `1->2->3->4->5->NULL` and `k = 2`,
 return `4->5->1->2->3->NULL`.

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
 
 ListNode* kthnode(ListNode* head, int k){
     if(head== NULL || head->next == NULL){
         return head;
     }
     
     ListNode* slow = head;
     ListNode* fast = head;
     while(fast !=NULL and k>0){
         fast = fast->next;
         k--;
     }
     while(fast->next!=NULL){
         fast = fast->next;
         slow = slow->next;
     }
     return slow;
 }
 
 
 
ListNode* Solution::rotateRight(ListNode* A, int B) {
    if(A == NULL || A->next ==NULL){
        return A;
    }
    
    int length = 0;
    ListNode* le = A;
    while(le!= NULL){
        le = le->next;
        length++;
    }
    B = B%length;
    if(B==0){
        return A;
    }
    
    ListNode* k = kthnode(A, B);
    ListNode* temp = k->next;
    ListNode* p = k;
    while(k->next!=NULL){
        k = k->next;
    }
    k->next = A;
    p->next = NULL;
    return temp
}
```