# Partition List | Interviewbit

Created: June 21, 2022 4:19 PM
Tags: Linked List
URL: https://www.interviewbit.com/problems/partition-list/

Given a linked list and a value x, partition it such that all nodes less than x come before nodes greater than or equal to x.

You should preserve the original relative order of the nodes in each of the two partitions.

For example,
 Given `1->4->3->2->5->2` and `x = 3`,
 return `1->2->2->4->3->5`.

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
 
 
ListNode* Solution::partition(ListNode* head, int x) {
    ListNode* list1 = new ListNode(0);
    ListNode* list2 = new ListNode(0);
    ListNode* l1 = list1;
    ListNode* l2 = list2;
    
    while(head){
        if(head->val<x){
            l1->next = head;
            l1 = l1->next;
        }
        else{
            l2->next = head;
            l2 = l2->next;
        }
        head = head->next;
    }
    
    l1->next = list2->next;
    l2->next = NULL;
    
    return list1->next;
}
```