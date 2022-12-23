# Insertion Sort List | Interviewbit

Created: June 21, 2022 5:34 PM
Tags: Linked List
URL: https://www.interviewbit.com/problems/insertion-sort-list/

Sort a linked list using insertion sort.

We have explained Insertion Sort at Slide 7 of [Arrays](http://www.interviewbit.com/courses/programming/topics/arrays/)

[Insertion Sort Wiki](http://en.wikipedia.org/wiki/Insertion_sort#Algorithm) has some details on Insertion Sort as well.

**Example :**

```
Input : 1 -> 3 -> 2

Return 1 -> 2 -> 3

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
 ListNode* Solution::insertionSortList(ListNode* head) {
    ListNode* ans = new ListNode(-1);
    ans->next = head;
    ListNode* curr = head->next;
    ListNode* prev = head;

    while(curr){
        if(curr->val >= prev->val){
            prev = curr;
            curr = curr->next;
            continue;
        }

        ListNode* temp = ans;
        while(curr->val > temp->next->val){
            temp = temp->next;
        }

        prev->next = prev->next->next;
        curr->next = temp->next;
        temp->next = curr;
        curr = prev->next;
    }
    return ans->next;
}
```

## My code

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
     if(head == NULL || head->next==NULL){
         return head;
     }
     
     ListNode* slow = head;
     ListNode* fast = head->next;
     while(fast!= NULL and fast->next != NULL){
         fast = fast->next->next;
         slow = slow->next;
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
     
     if(a->val > b->val){
         b->next = merge(a, b->next);
         a = b;
     }
     else{
         a->next = merge(a->next, b);
     }
     return a;
 }
 
 
 
 ListNode* mergersort(ListNode* head){
     if(head == NULL ||head->next == NULL){
         return head;
     }
     
     ListNode* mid = midpoint(head);
     ListNode* a = head;
     ListNode* b = mid->next;
     mid->next = NULL;
     a = mergersort(a);
     b = mergersort(b);
     ListNode* e = merge(a,b);
     return e;
 }
 
 
ListNode* Solution::insertionSortList(ListNode* A) {
    return mergersort(A);
}
```