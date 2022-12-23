# Reorder List | Interviewbit

Created: June 22, 2022 12:06 AM
Tags: Linked List
URL: https://www.interviewbit.com/problems/reorder-list/

Given a singly linked list

```
    L: L0 → L1 → … → Ln-1 → Ln,

```

reorder it to:

```
    L0 → Ln → L1 → Ln-1 → L2 → Ln-2 → …

```

You must do this in-place without altering the nodes’ values.

For example,
 Given `{1,2,3,4}`, reorder it to `{1,4,2,3}`.

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
ListNode* Solution::reorderList(ListNode* head) {
    if(head==NULL || head->next==NULL || head->next->next == NULL){
        return head;
    }
    
    ListNode* curr = head;
    bool flag = true;
    while(curr!= NULL){
        if(flag){
            ListNode* runn = curr;
            ListNode* lastpre = NULL;
            while(runn->next != NULL){
                runn = runn->next;
                if(runn->next != NULL and runn->next->next == NULL){
                    lastpre = runn;
                }
            }
            if(lastpre == NULL){
                break;
            }
            
            lastpre->next = NULL;
            ListNode* prev = curr->next;
            
            curr->next = runn;
            runn->next = prev;
            flag = false;
        }
        else{
            flag = true;
        }
        
        
        curr = curr->next;
        
    }
    return head;
```

```cpp
ListNode * findMid(ListNode *head){
    ListNode * slow = head , *fast = head->next;
    while(fast && fast->next){
        slow = slow->next;
        fast = fast->next->next;
    }  
    return slow;
}
ListNode *rev(ListNode *head){
    ListNode *p = NULL , *c = head , *n = NULL;
    while(c){
        n = c->next;
        c->next = p;
        p = c;
        c = n;
    }
    return p;
}
ListNode* Solution::reorderList(ListNode* A) {
    ListNode *mid = findMid(A);
    // return mid;
    ListNode *temp1 = mid->next;
    mid->next = NULL;
    temp1 = rev(temp1);
    // return temp1;
    ListNode *temp = A;
    while(temp && temp1){
        ListNode *temp2 = temp->next  ,  *temp3 = temp1->next;
        temp->next = temp1;
        temp1->next = temp2;
        temp = temp2;
        temp1 = temp3;
    }
    return A;
}
```

## Interview bit Code

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
ListNode* Solution::rotateRight(ListNode* A, int B) {
    ListNode* ret, *curr, *prev;
    int temp, length = 0;
    curr = A;
    prev = A;
    while(curr) {
        ++length;
        curr = curr->next;
    }
    if (length == 0 || B%length == 0) {
        return A;
    }
    curr = A;
    temp = B%length;
    while(temp-- > 0 ) {
        curr = curr->next;
    }
    while (curr->next) {
        curr = curr->next;
        prev = prev->next;
    }
    ret = prev->next;
    prev->next = NULL;
    curr->next = A;
    return ret;
}
```