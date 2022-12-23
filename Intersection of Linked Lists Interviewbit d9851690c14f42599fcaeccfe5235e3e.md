# Intersection of Linked Lists | Interviewbit

Created: June 21, 2022 1:19 PM
Tags: Linked List
URL: https://www.interviewbit.com/problems/intersection-of-linked-lists/

Write a program to find the node at which the intersection of two singly linked lists begins.

For example, the following two linked lists:

```

A:          a1 → a2
                   ↘
                     c1 → c2 → c3
                   ↗
B:     b1 → b2 → b3

```

begin to intersect at node c1.

> 
> 
> 
> **Notes:**
> 
> - If the two linked lists have no intersection at all, return null.
> - The linked lists must retain their original structure after the function returns.
> - You may assume there are no cycles anywhere in the entire linked structure.
> - Your code should preferably run in O(n) time and use only O(1) memory.

**Problem approach completely explained :**

Complete code in the hints section.

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
ListNode* Solution::getIntersectionNode(ListNode* A, ListNode* B) {
    // Do not write main() function.
    // Do not read input, instead use the arguments to the function.
    // Do not print the output, instead return values as specified
    // Still have a doubt. Checkout www.interviewbit.com/pages/sample_codes/ for more details
    ListNode* a = A;
    ListNode* b = B;
    int counta = 0;
    int countb = 0;
    while(a != NULL){
        counta++;
        a = a->next;
    }
    while(b!=NULL){
        countb++;
        b = b->next;
    }
    a = A;
    b = B;
    if(counta>countb){
        int d = counta-countb;
        while(d>0){
            a = a->next;
            d--;
        }
        
        while(a!=NULL and b!=NULL){
            if(a==b){
                return a;
            }
            a = a->next;
            b = b->next;
        } 
    }
    else{
        int d = countb-counta;
        while(d>0){
            b = b->next;
            d--;
        }
        
        while(a!=NULL and b!=NULL){
            if(a==b){
                return b;
            }
            a = a->next;
            b = b->next;
        }
    }
    
    return NULL;
}
```