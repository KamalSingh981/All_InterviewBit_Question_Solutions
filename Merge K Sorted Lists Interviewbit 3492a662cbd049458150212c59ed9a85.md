# Merge K Sorted Lists | Interviewbit

Created: July 18, 2022 1:41 PM
Tags: Heap
URL: https://www.interviewbit.com/problems/merge-k-sorted-lists/

Merge k sorted linked lists and return it as one sorted list.

**Example :**

```
1 -> 10 -> 20
4 -> 11 -> 13
3 -> 8 -> 9

```

will result in

```
1 -> 3 -> 4 -> 8 -> 9 -> 10 -> 11 -> 13 -> 20

```

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
 
 
#define pi pair<int, ListNode*>

ListNode* Solution::mergeKLists(vector<ListNode*> &A) {
    // Do not write main() function.
    // Do not read input, instead use the arguments to the function.
    // Do not print the output, instead return values as specified
    // Still have a doubt. Checkout www.interviewbit.com/pages/sample_codes/ for more details
    
    priority_queue<pi, vector<pi>, greater<pi>> pq;

    // inserted all the first element of every list
    for(int i = 0; i<A.size(); i++){
        if(A[i]){
            pq.push({A[i]->val, A[i]});
        }
    }
    
    pair<int, ListNode*> p;
    ListNode*d = new ListNode(-1);
    ListNode*t = d;
    while(!pq.empty()){
        t->next = pq.top().second;
        t = t->next;
        p = pq.top();
        pq.pop();
        
        if(p.second->next){
            pq.push({p.second->next->val, p.second->next});
        } 
    }
    
    return d->next;    
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
 
 
struct mycomp{
    
    bool operator() (ListNode* a, ListNode* b){
        
        return a->val > b->val;
    }
};

ListNode* Solution::mergeKLists(vector<ListNode*> &A) {
    // Do not write main() function.
    // Do not read input, instead use the arguments to the function.
    // Do not print the output, instead return values as specified
    // Still have a doubt. Checkout www.interviewbit.com/pages/sample_codes/ for more details
      
        priority_queue<ListNode*, vector<ListNode*>, mycomp> pq;
        
        for(ListNode*x:A){
            if(x){
            pq.push(x);
            }
        }  
        
        ListNode* head = NULL;
        ListNode* tail = NULL;
        while(!pq.empty()){
            ListNode* x = pq.top();
            
            pq.pop();
            if(head == NULL){             
                tail = x;
                head = tail;
            }          
            else{
                
                tail->next = x;
                tail = x;
            }
            if(x->next) pq.push(x->next);
        }
    return head;       
}
```