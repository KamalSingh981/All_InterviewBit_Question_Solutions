# Palindrome List | Interviewbit

Created: June 21, 2022 6:25 PM
Tags: Linked List
URL: https://www.interviewbit.com/problems/palindrome-list/

Given a singly linked list, determine if its a palindrome. Return 1 or 0 denoting if its a palindrome or not, respectively.

**Notes**:

- Expected solution is linear in time and constant in space.

For example,

```cpp
ListNode* reverse(ListNode* &head){
    if(head == NULL || head-> next == NULL){
        return head;
    }
    ListNode* shead = reverse(head->next);
    head->next->next = head;
    head->next = NULL;
    return shead;
}
ListNode* midpoint(ListNode* head){
    if(head == NULL || head->next == NULL){
        return head;
    }
    
    ListNode* slow = head;
    ListNode* fast = head->next;
    while(fast != NULL and fast->next !=NULL){
        slow = slow->next;
        fast = fast->next->next;
    }
    return slow;
}

int Solution::lPalin(ListNode* head) {
    if(head == NULL || head->next == NULL){
        return 1;
    }
    ListNode* midp = midpoint(head);
    ListNode* r = reverse(midp);
    while((r->val == head->val) and head!=midp){
        r = r->next;
        head = head->next;
    }
    if(r->val == head->val){
        return 1;
    }    
    return 0;
}
```

## Using Arrays

```cpp
int Solution::lPalin(ListNode* head) {
    if(head == NULL || head->next == NULL){
        return 1;
    }
    vector<int> ans;
    while(head){
        ans.push_back(head->val);
        head = head->next;
    }
    int n = ans.size();
    for(int i = 0; i<n/2; i++){
        if(ans[i] != ans[n-1-i]){
            return 0;
        }
    }
    return 1;
}
```