# Swap List Nodes in pairs | Interviewbit

Created: June 22, 2022 2:23 AM
Tags: Linked List
URL: https://www.interviewbit.com/problems/swap-list-nodes-in-pairs/

Given a linked list, swap every two adjacent nodes and return its head.

For example,
 Given `1->2->3->4`, you should return the list as `2->1->4->3`.

Your algorithm should use only constant space. You may not modify the values in the list, only nodes itself can be changed.

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
ListNode* Solution::swapPairs(ListNode* head) {
       ListNode* prevptr = NULL;
    ListNode* currptr = head;
    ListNode* nextptr;
    int count = 0;
    while(currptr!=NULL and count<2){
        nextptr = currptr->next;
        currptr->next = prevptr;
        prevptr= currptr;
        currptr = nextptr;
        count++;
    }
    
    if(nextptr!=NULL){
        head->next = swapPairs(nextptr);
    }
    return prevptr;
}
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
ListNode* Solution::swapPairs(ListNode* head) {
    
    
    ListNode* first = head;
    ListNode* dummy = new ListNode(-1);
    ListNode* prev =  dummy;
    prev -> next = head;
    
    
    while(first and first->next){
        ListNode* second = first->next;
        ListNode* future = first->next->next;
        second->next = first;
        prev->next = second;
        first->next = future;
        prev = first;
        first = future;
    }
    
    return dummy->next;
}
```