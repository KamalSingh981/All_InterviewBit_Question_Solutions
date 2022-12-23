# SUBTRACT | Interviewbit

Created: June 21, 2022 2:28 AM
Tags: Linked List
URL: https://www.interviewbit.com/problems/subtract/

Given a singly linked list, modify the value of **first half nodes** such that :

- 1st node’s new value = the last node’s value - first node’s current value
- 2nd node’s new value = the second last node’s value - 2nd node’s current value,

and so on …

> 
> 
> 
> **NOTE :**
> 
> - If the length L of linked list is odd, then the first half implies at first floor(L/2) nodes. So, if L = 5, the first half refers to first 2 nodes.
> - If the length L of linked list is even, then the first half implies at first L/2 nodes. So, if L = 4, the first half refers to first 2 nodes.

**Example :**

Given linked list `1 -> 2 -> 3 -> 4 -> 5`,

You should return `4 -> 2 -> 3 -> 4 -> 5`
 as

```
for first node, 5 - 1 = 4
for second node, 4 - 2 = 2

```

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

ListNode* reverse(ListNode* node) {
    if(node->next == NULL) {
        return node;
    } else {
        ListNode* nNext = node->next;
        ListNode* rev = reverse(nNext);
        nNext->next = node;
        node->next = NULL;
        return rev;
    }
}

int size(ListNode* node) {
    if(node == NULL) return 0;
    return 1 + size(node->next);
}
ListNode* Solution::subtract(ListNode* A) {
    if(A->next == NULL) return A;
    ListNode* curr = A;
    // find half way point
    int n = size(A);
    int c = 0;
    while(curr != NULL && c<(n/2)) {
        curr = curr->next;
        c++;
    }

    ListNode* revcurr = reverse(curr);
    
    ListNode *i,*j;
    i = A;
    j = revcurr;
    while(i!= NULL && j!= NULL) {
        
         i->val = j->val - i->val;
         if(i->next == curr) break;
         i = i->next;
         j = j->next;    
    }

    revcurr = reverse(revcurr);

    return A;

}
```