# Add Two Numbers as Lists | Interviewbit

Created: June 22, 2022 12:38 AM
Tags: Linked List
URL: https://www.interviewbit.com/problems/add-two-numbers-as-lists/

You are given two linked lists representing two non-negative numbers. The digits are stored in **reverse order** and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

Input: `(2 -> 4 -> 3)` + `(5 -> 6 -> 4)`
 Output: `7 -> 0 -> 8`

```
    342 + 465 = 807

```

Make sure there are no trailing zeros in the output list
 So, `7 -> 0 -> 8 -> 0` is not a valid response even though the value is still 807.

Note:You only need to implement the given function. Do not read input, instead use the arguments to the function. Do not print the output, instead return values as specified. Still have a question? Checkout [Sample Codes](https://www.interviewbit.com/pages/sample_codes/) for more details.

My Code

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
ListNode* Solution::addTwoNumbers(ListNode* A, ListNode* B) {
    if(A==NULL){
        return B;
    }
    if(B == NULL){
        return A;
    }
    
    
    ListNode* head =  new ListNode(0);
    ListNode* p = head;
    int carry = 0;
    while(A!=NULL || B!=NULL){
        int sum = carry;
        if(A!=NULL){
            sum += A->val;
            A = A->next;
        }
        if(B!=NULL){
            sum += B->val;
            B = B->next;
        } 
        p->val = sum%10;
        carry = sum/10;
        p->next = new ListNode(0);
        p = p->next;
    }
    p->val = carry;
    p = head;
    int count = 0;
    int n =0;
    while(p !=NULL){
        if(p->val == 0){
            count++;
        }
        else{
            count = 0;
        }
        p = p->next;
        n++;
        
    }
    p = head;
    n = n - count-1;
    while(n--){
        p = p->next;
    }
    p->next = NULL;
    
    return head;
}
```

## Code from Discussion

```cpp
ListNode* Solution::addTwoNumbers(ListNode* A, ListNode* B) {
if(A==NULL)return B;
else if(B==NULL)return A;

int carry=0;
int sum=0;

ListNode*dummy =new ListNode(0);
ListNode*head=dummy;

while(A!=NULL || B!=NULL || carry==1)
{ sum=0;
if(A!=NULL)
{
sum+=A->val;
A=A->next;
}
if(B!=NULL)
{
sum+=B->val;
B=B->next;
}
sum=sum+carry;
carry=sum/10;

head->next=new ListNode(sum%10);
head=head->next;
}
return dummy->next;
}
```