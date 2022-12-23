# Numbers of length N and value less than K | Interviewbit

Created: May 22, 2022 3:31 PM
Tags: Math
URL: https://www.interviewbit.com/problems/numbers-of-length-n-and-value-less-than-k/

Given a set of digits (A) in sorted order, find how many numbers of length B are possible whose value is less than number C.

**NOTE: All numbers can only have digits from the given set.**

**Examples:**

```
Input:
  0 1 5

  1

  2

Output:

  2 (0 and 1 are possible)

```

**Constraints:**

```
1 <= B <= 9, 0 <= C <= 1e9 & 0 <= A[i] <= 9

```

```cpp
int Solution::solve(vector<int> &A, int B, int C) {
    if(A.size()==0){return 0;}
    
    int temp=C,count=0,ans=0;
    while(temp){
        count++;
        temp/=10;
    }       
            
    if(count<B){return 0;}
    else if(count>B){
        if(A[0]==0){
            ans=(A.size()-1)*pow(A.size(),B-1);
        }   
        else{
            ans=pow(A.size(),B);
        }   
        if(B==1 && A[0]==0){ans++;}
        return ans;
    }       
    else{   
       if(B==1){
           for(int i=0;i<A.size();i++){if(A[i]<C){ans++;}}
       }    
       else{
           vector<int> temp(B);
           for(int i=B-1;i>=0;i--){
               temp[i]=C%10;
               C=C/10;
           }
            
           count=0; 
           for(int i=0;i<A.size();i++){
               if(A[i]==0){continue;}
                if(A[i]>temp[0]){break;}
                count++;
           }    
           ans+=(count)*(pow(A.size(),B-1));
           // this ans contain some extra values--
           int flag=0,j=0;
           for(int i=0;i<A.size();i++){if(A[i]==temp[j]){flag=1;}}
           j++;
           while(flag==1 && j<=B-1){
               flag=0;
               int countx=0;
               for(int i=0;i<A.size();i++){if(A[i]>temp[j]){countx++;} if(A[i]==temp[j]){flag=1;}}
               ans-=((countx)*(pow(A.size(),B-j-1)));
           j++;
           }
           if(j==B && flag==1){ans--;}
       }    
    }       
    return ans;
}
```