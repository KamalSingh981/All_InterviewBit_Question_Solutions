# Copy List | Interviewbit

Created: July 16, 2022 2:03 AM
Tags: Hashing
URL: https://www.interviewbit.com/problems/copy-list/

A linked list is given such that each node contains an additional random pointer which could point to any node in the list or `NULL`.

Return a deep copy of the list.

**Example**

Given list

```
   1 -> 2 -> 3

```

with random pointers going from

You should return a deep copy of the list. The returned answer should not contain the same node as the original list, but a copy of them. The pointers in the returned list should not link to any node in the original input list.

```cpp
RandomListNode* Solution::copyRandomList(RandomListNode* A) {
    
    RandomListNode* curr = A;
    map<RandomListNode*, RandomListNode*> m;
    while(curr != NULL){
        RandomListNode* copy = new RandomListNode(curr->label);
        m[curr] = copy;
        curr = curr->next;
    }
    curr  = A;
    while(curr != NULL){
        RandomListNode* copy = m[curr];
        copy->next = m[curr->next];
        copy->random = m[curr->random];
        curr = curr->next;
    }
    return m[A};
}
```