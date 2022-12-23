# Reverse Alternate K Nodes | Interviewbit

Created: June 21, 2022 10:24 PM
Tags: Linked List
URL: https://www.interviewbit.com/problems/reverse-alternate-k-nodes/

**Problem Description**

Given a linked list **A** of length **N** and an integer **B**.

You need to reverse every alternate **B** nodes in the linked list **A**.

**Problem Constraints**

**Input Format**

First argument is the head pointer of the linkedlist **A**.

Second argument is an integer **B**.

**Output Format**

Return the head pointer of the final linkedlist as described.

**Example Input**

Input 1:

```
 A = 3 -> 4 -> 7 -> 5 -> 6 -> 6 -> 15 -> 61 -> 16
 B = 3

```

Input 2:

```
 A = 1 -> 4 -> 6 -> 6 -> 4 -> 10
 B = 2

```

**Example Output**

Output 1:

```
 7 -> 4 -> 3 -> 5 -> 6 -> 6 -> 16 -> 61 -> 15

```

Output 2:

```
 4 -> 1 -> 6 -> 6 -> 10 -> 4

```

**Example Explanation**

Explanation 1:

```
 The linked list contains 9 nodes and we need to reverse alternate 3 nodes.
 First sublist of length 3  is 3 -> 4 -> 7 so on reversing it we get 7 -> 4 -> 3.
 Second sublist of length 3 is 5 -> 6 -> 6 we don't need to reverse it.
 Third sublist of length 3 is 15 -> 61 -> 16 so on reversing it we get 16 -> 61 -> 15.

```

Explanation 2:

```
 The linked list contains 6 nodes and we need to reverse alternate 2 nodes.
 First sublist of length 2 is 1 -> 4 so on reversing it we get 4 -> 1.
 Second sublist of length 2 is 6 -> 6 we don't need to reverse it.
 Third sublist of length 2 is 4 -> 10 so on reversing it we get 10 -> 4.

```

```cpp
ListNode* Solution::solve(ListNode* head, int k) {
    if(k==1)
    {
        return head;
    }
   
    if(head==NULL || head->next==NULL)
    {
        return head;
    }
   
    ListNode* p=NULL , *prev=NULL , *curr=head , *newhead=NULL;
   
    int count=0;
   
    bool flag=false;
   
    bool f=false;
   
    while(curr)
    {
        int count=0;
        ListNode* start=curr;
       
        if(flag==false)
        {
            while(curr && count<k)
            {
                ListNode* next=curr->next;
                curr->next=prev;
                prev=curr;
                curr=next;
                count++;
                flag=true;
            }
            if(p!=NULL)
            {
                p->next=prev;
            }
            if(f==false)
            {
                newhead=prev;
                f=true;
            }
            start->next=curr;
          //  p=start;
        }
        else
        {
            while(curr && count<k)
            {
                prev=curr;
                curr=curr->next;
                count++;
                flag=false;
            }
            p=prev;
        }
    }
    return newhead;
}
```