# Even Reverse | Interviewbit

Created: June 22, 2022 1:35 AM
Tags: Linked List
URL: https://www.interviewbit.com/problems/even-reverse/

**Problem Description**

Given a linked list **A** , reverse the order of all nodes at even positions.

**Problem Constraints**

**Input Format**

First and only argument is the head of the Linked-List A.

**Output Format**

Return the head of the new linked list.

**Example Input**

Input 1:

```
A = 1 -> 2 -> 3 -> 4

```

Input 2:

```
A = 1 -> 2 -> 3

```

**Example Output**

Output 1:

```
 1 -> 4 -> 3 -> 2

```

Output 2:

```
 1 -> 2 -> 3

```

**Example Explanation**

Explanation 1:

```
Nodes are positions 2 and 4 have been swapped.

```

Explanation 2:

```
No swapping neccassary here.

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
ListNode* Solution::solve(ListNode* head) {
    if(head==NULL || head->next ==NULL){
        return head;
    }
    ListNode* A = head;
    
    vector<int> ans;
    int le = 0;
    while(head!=NULL){
        ans.push_back(head->val);
        head = head->next;
        le++;
    }
    
    if(le%2 == 0){
        for(int i = 1; i<(le/2+1);  i += 2){
            swap(ans[i], ans[le-i]);
        }
    }
    else{
        for(int i = 1; i<(le/2+1); i += 2){
            swap(ans[i], ans[le-i-1]);
        }
    }
    head = A;
    for(int i = 0; i<le; i++){
        head->val = ans[i];
        head = head->next;
    }
    return A;
}
```