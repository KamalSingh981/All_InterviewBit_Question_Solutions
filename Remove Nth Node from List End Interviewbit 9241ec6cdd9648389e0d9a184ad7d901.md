# Remove Nth Node from List End | Interviewbit

Created: June 21, 2022 5:05 PM
Tags: Linked List
URL: https://www.interviewbit.com/problems/remove-nth-node-from-list-end/

Given a linked list, remove the nth node from the end of list and return its head.

For example,
 Given linked list: `1->2->3->4->5`, and `n = 2`.
 After removing the second node from the end, the linked list becomes `1->2->3->5`.

> 
> 
> 
> **Note:**
> 
> - If n is greater than the size of the list, remove the first node of the list.

Try doing it using constant additional space.

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
 void deleteAtHead(ListNode*&head){
    if(head == NULL){
        return;
    }
    ListNode*temp = head->next;
    delete head;
    head = temp;
}

 void deleteNode(ListNode* &head){
     ListNode* temp = head->next;
     head->next = head->next->next;
     delete temp;
 }
ListNode* Solution::removeNthFromEnd(ListNode* head, int k) {
    ListNode* slow =  head;
    ListNode* fast = head;
    int count  = 1;
    while(fast->next != NULL and count<k){
        fast = fast->next;
        count++;
    }
    if(fast->next == NULL){
        deleteAtHead(head);
        return head;
    }
    fast = fast->next;
    while(fast->next != NULL){
        fast = fast->next;
        slow = slow->next;
    }
    deleteNode(slow);
    return head;
}
```

## Other way implementation

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
ListNode* Solution::removeNthFromEnd(ListNode* head, int k) {
    ListNode* slow =  head;
    ListNode* fast = head;
    int count  = 0;
    while(fast->next != NULL and count<k){
        fast = fast->next;
        count++;
    }
    if(fast->next == NULL){
        return head->next;
    }
    while(fast->next != NULL){
        fast = fast->next;
        slow = slow->next;
    }
    slow->next = slow->next->next;
    return head;
}
```