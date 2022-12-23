# Min Cost Path | Interviewbit

Created: July 27, 2022 12:41 PM
Tags: Graphs
URL: https://www.interviewbit.com/problems/min-cost-path/

**Problem Description**

You are given a **A*B** character matrix named **C**. Every cell in **C** has a character **U,R,L or D** indicating up,right,left and down.*

*Your target is to go from **top left corner** to the **bottom right corner** of the matrix.*

*But there are some restrictions while moving along the matrix: 
• If you follow what is written in the cell then you can move freely. 
• But if you don't follow what is written in the cell then you have to pay 1 unit of cost. 
Like: If a cell contains character **U** and you go **right** instead of **Up** you have to pay 1 unit of cost. 
So your task is to find the **minimum cost** to go from top-left corner to the bottom-right corner.*

*Problem Constraints*

* 1 <= A,B <= 103  C[i][j] can be either **U,R,L or D**.*

*Input Format*

*
•  First Argument represents a integer A (number of rows).  
•  Second Argument represents a integer B (number of columns).  
•  Third Argument represents a string array **C** which contains **A** strings each of length **B**.*  

*Output Format*

*Return an integer denoting the minimum cost to travel from top-left corner to bottom-right corner.*

*Example Input*

*Input:1 

 `A = 3
 B = 3
 C = ["RRR","DDD","UUU"]`
          
Input:2 

 `A = 1
 B = 4
 C = ["LLLL"]`*

*Example Output*

*Output-1 : 

 `1`          
Output-2 : 

 `3`*

*Example Explanation*

- 

Explanation for Input-1:

```
 Matrix looks like: RRR
                    DDD
                    UUU
 We go right two times and down two times.
 So from top-right cell we are going down though right is given so this incurs a cost of 1.

```

Explanation for Input-2:

```
 Matrix looks like: LLLL
 We go right three times.

```

```cpp
// Intuition -> there is no dp , because a node or cell can be visited multiple times

// so what we have to do is , we update the distance value each time

// and also put that cost  and index into the pq , as it can afftect the

// cost of many path , it is possible that many path may

// conntains it in its way

#define vv vector<int>

int Solution::solve(int m , int n , vector<string> &grid) {
   
    // Dijkstra's Algorithm
   
    priority_queue< vv , vector<vv> , greater<vv>> pq;
   
    pq.push({0 , 0 , 0});
   
    int dx[4]={-1 , 1 , 0 , 0};
    int dy[4]={0 , 0  , -1 , 1};
   
    // UP , DOWN , LEFT , RIGHT
   
   
   
    vector<vector<int>> dist(m , vector<int>(n , INT_MAX));
   
    dist[0][0]=0;
   
    while(!pq.empty())
    {
        auto arr=pq.top();
        pq.pop();
       
        int cost=arr[0];
        int i=arr[1];
        int j=arr[2];
       
        int ind;
       
      if(grid[i][j]=='U')
      {
          ind=0;
      }
     
      if(grid[i][j]=='D')
      {
          ind=1;
      }
     
      if(grid[i][j]=='L')
      {
          ind=2;
      }
     
      if(grid[i][j]=='R')
      {
          ind=3;
      }
     
      for(int k=0;k<4;k++)
      {
          int newi=i+dx[k];
          int newj=j+dy[k];
         
          if(newi<0 || newj<0 || newi>=m || newj>=n)
          {
              continue;
          }
         
          if(k==ind && dist[newi][newj]>cost)
          {
              dist[newi][newj]=cost;
              pq.push({cost , newi , newj});
          }
          else
          if(dist[newi][newj]>1+cost)
          {
              dist[newi][newj]=cost+1;
              pq.push({cost+1 , newi , newj});
          }
      }
       
    } 
    return dist[m-1][n-1];  
}
```