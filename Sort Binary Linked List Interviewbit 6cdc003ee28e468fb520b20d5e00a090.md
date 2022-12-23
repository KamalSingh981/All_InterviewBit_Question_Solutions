# Sort Binary Linked List | Interviewbit

Created: June 21, 2022 3:00 AM
Tags: Linked List
URL: https://www.interviewbit.com/problems/sort-binary-linked-list/

**Problem Description**

Given a Linked List **A** consisting of **N** nodes.

The Linked List is binary i.e data values in the linked list nodes consist of only **0's** and **1's**.

You need to sort the linked list and return the new linked list.

**NOTE:**

- Try to do it in constant space.

**Problem Constraints**

1 <= N <= 105

A.val = 0 or A.val = 1

**Input Format**

First and only argument is the head pointer of the linkedlist **A**.

**Output Format**

Return the head pointer of the new sorted linked list.

**Example Input**

Input 1:

```
 1 -> 0 -> 0 -> 1

```

Input 2:

```
 0 -> 0 -> 1 -> 1 -> 0

```

**Example Output**

Output 1:

```
 0 -> 0 -> 1 -> 1

```

Output 2:

```
 0 -> 0 -> 0 -> 1 -> 1

```

**Example Explanation**

Explanation 1:

```
 The sorted linked list looks like:
  0 -> 0 -> 1 -> 1

```

Explanation 2:

```
 The sorted linked list looks like:
  0 -> 0 -> 0 -> 1 -> 1

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
 
 ListNode* merge(ListNode* a, ListNode* b){
     if(a==NULL){
         return b;
     }
     if(b == NULL){
         return a;
     }
     
     ListNode* c;
     if(a->val < b->val){
         c = a;
         c->next = merge(a->next, b);
     }
     else{
         c= b;
         c->next = merge(a, b->next);
     }
     return c;
     
 }
 ListNode* getnode(ListNode* a){
     if(a == NULL || a-> next == NULL ){
         return a;
     }
     
     ListNode* slow = a;
     ListNode* fast = a->next;
     while(fast!=NULL && fast-> next != NULL){
         slow = slow->next;
         fast= fast->next->next;
     }
     return slow;
     
     
 }
 
 ListNode* mergesort(ListNode* a){
     if(a == NULL || a->next ==NULL){
         return a;
     }
     //rec case
    // break
    ListNode* mid = getnode(a);
    ListNode*c = a;
    ListNode*d = mid->next;
    mid->next = NULL;

    c = mergesort(c);
    d = mergesort(d);
    ListNode* e = merge(c,d);
    return e;
 }
 
 
ListNode* Solution::solve(ListNode* A) {
    return mergesort(A);
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
  
 
ListNode* Solution::solve(ListNode* A) {
    int count0 = 0;
    int count1 = 0;
    ListNode* temp = A;
    while(temp !=NULL){
        if(temp->val == 0){
            count0++;
        }
        else{
            count1++;
        }
        temp = temp->next;
    }
    temp = A;
    // temp = temp->next;
    while(count0+count1 != 0){
        if(count0>0){
            temp-> val = 0;
            count0--;
        }
        else{
            temp-> val = 1;
            count1--;
        }
        temp = temp->next;
        
    }
    return A;
}
```