# Ways to color a 3xN Board | Interviewbit

Created: August 8, 2022 3:48 AM
Tags: Dynamic Programming
URL: https://www.interviewbit.com/problems/ways-to-color-a-3xn-board/

Given a **3 x A** board, find the number of ways to color it using at most **4** colors such that no **2** adjacent boxes have same color.

Diagonal neighbors are not treated as adjacent boxes.

Return the ways modulo **109 + 7** as the answer grows quickly.

**Input Format:**

```
The first and the only argument contains an integer, A.

```

**Output Format:**

```
Return an integer representing the number of ways to color the board.

```

**Constraints:**

```
1 <= A < 100000

```

**Examples:**

```cpp
int Solution::solve(int A) {
    long long c2 = 12;
    long long c3 = 24;
    long long mod = 1e9 + 7;
    for(int i = 2; i<=A; i++){
        long long temp = (7*c2%mod + c3*5%mod)%mod;
        c3 = (10*c2%mod + 11*c3%mod)%mod;
        c2 = temp%mod;
    }
    return (c2+c3)%mod;
    
}
```

Iterative solution 

```cpp
#define mod 1000000007
#define ll long long

struct triplet{
	int x, y, z;
};

vector<triplet> trip;  //vector of 36 triplets

void fillTriplets(){
	//trip vector contain the triplets of color that can be used to paint a certain column
       trip.clear();
	for(int i=0; i<4; i++){
		for(int j=0; j<4; j++){
			for(int k=0; k<4; k++){
				if(i!=j && j!=k) trip.push_back({i,j,k});
			}
		}
	}
}

int dp[4][4][4][100005];

bool isCompatible(const triplet& t1,  const triplet& t2){
	//check if triplets t1 and t2 are compatible
	if(t1.x==t2.x || t1.y==t2.y || t1.z==t2.z ){
		return 0;
	}
	return 1;
}

int Solution::solve(int n){
        fillTriplets();
	if(n<=0) return -1;
	
       //Bottom-up dp
	for(int i=1; i<=n; i++){
		for(int j=0; j<36; j++){
			if(i==1) dp[trip[j].x][trip[j].y][trip[j].z][i] = 1;
			else{
				ll temp = 0;
				
				for(int k=0; k<36; k++){
					if(isCompatible(trip[j], trip[k])){
						temp += dp[trip[k].x][trip[k].y][trip[k].z][i-1];
						temp %= mod;
					}
				}
				dp[trip[j].x][trip[j].y][trip[j].z][i] = temp;
			}
		}
	}
	
	ll ans = 0;
	for(int i=0; i<trip.size(); i++){
		ans = (ans + dp[trip[i].x][trip[i].y][trip[i].z][n])%mod;
	}
        int res = ans;

	return res;
}
```

[https://www.youtube.com/watch?v=wInXbAHi72g](https://www.youtube.com/watch?v=wInXbAHi72g)