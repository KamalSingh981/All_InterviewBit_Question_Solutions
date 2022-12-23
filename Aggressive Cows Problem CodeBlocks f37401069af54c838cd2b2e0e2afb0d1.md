# Aggressive Cows Problem | CodeBlocks

Created: June 18, 2022 2:47 PM
Tags: Binary Search

```

bool canPlaceCows(int stalls[], int n, int c, int min_sep){
    int last_cow = stalls[0];
    int cnt = 1;
    for(int i = 1; i<n; i++){
        if(stalls[i] - last_cow>=min_sep){
            last_cow = stalls[i];
            cnt++;
            if(cnt == c){
                return true;
            }
        }
    }
    return false;
}

int min(){
// For solving questions using binary search we need to about a search space which should to monotonically increasing or decreasing.
// Then we can get do binary search and check whether the element in the search space is valid or not.
// If valid does it satisfy the condition.

// code
int stalls[] = {1,2,4,8,9};
int n =5;
int cows =3;
// binary search algorithm
int s=0;
int e = stalls[n-1] - stalls[0];

int ans =0;
while(s<=e){
    int mid = (s+e)/2;
bool cowsRakhPaye = canPlaceCows(stalls,n,cows,mid);
if(cowsRakhPaye){
        ans = mid;
s = mid +1;
}
    else{
        e = mid -1;
}
    return ans;
}

}
```