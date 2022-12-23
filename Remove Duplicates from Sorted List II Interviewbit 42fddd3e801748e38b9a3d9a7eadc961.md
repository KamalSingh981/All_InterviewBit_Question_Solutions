# Remove Duplicates from Sorted List II | Interviewbit

Created: June 21, 2022 7:10 PM
Tags: Linked List
URL: https://www.interviewbit.com/problems/remove-duplicates-from-sorted-list-ii/

Given a sorted linked list, delete all nodes that have duplicate numbers, leaving only distinct numbers from the original list.

For example,
 Given `1->2->3->3->4->4->5`, return `1->2->5`.
 Given `1->1->1->2->3`, return `2->3`.

Note:You only need to implement the given function. Do not read input, instead use the arguments to the function. Do not print the output, instead return values as specified. Still have a question? Checkout [Sample Codes](https://www.interviewbit.com/pages/sample_codes/) for more details.

```cpp
ListNode* Solution::deleteDuplicates(ListNode* A) {

    if(!A || !A->next) return A;
    ListNode* i, *j;
    ListNode* ans = new ListNode(INT_MAX);
    ans->next = A;
    i = ans;
    int c=0;
    while(i && i->next){
        j = i->next;
        c =0;
        int val = j->val;
        while(j && j->val == val){
                c++;
                j = j->next;
        }
        if(c==1){
            i = i->next;
        }
        else{
            i->next = j;
        }
    }
    return ans->next;
}
```

```cpp
ListNode* Solution::deleteDuplicates(ListNode* head) {
    ListNode* temphead = new ListNode(0);
    temphead->next = head;
    ListNode* temp = head;
    ListNode* prev = temphead;
    while(temp!=NULL){
        while(temp ->next !=NULL && temp->val == temp->next->val){
            temp = temp->next;
        }
        if(prev->next==temp) prev = prev->next;
        else{
            prev->next = temp->next;
        }
        temp = temp->next;
    }
    return temphead->next;
}
```