# K reverse linked list | Interviewbit

Created: June 22, 2022 1:06 AM
Tags: Linked List
URL: https://www.interviewbit.com/problems/k-reverse-linked-list/

Given a singly linked list and an integer *K*, reverses the nodes of the

list *K* at a time and returns modified linked list.

> 
> 
> 
> **NOTE :** The length of the list is divisible by K
> 

**Example :**

Given linked list `1 -> 2 -> 3 -> 4 -> 5 -> 6` and K=2,

You should return `2 -> 1 -> 4 -> 3 -> 6 -> 5`

Try to solve the problem using constant extra space.

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
ListNode* Solution::reverseList(ListNode* head, int B) {
    
    ListNode* prevptr = NULL;
    ListNode* currptr = head;
    ListNode* nextptr;
    int count = 0;
    while(currptr!=NULL and count<B){
        nextptr = currptr->next;
        currptr->next = prevptr;
        prevptr= currptr;
        currptr = nextptr;
        count++;
    }
    
    if(nextptr!=NULL){
        head->next = reverseList(nextptr, B);
    }
    return prevptr;
    
}
```