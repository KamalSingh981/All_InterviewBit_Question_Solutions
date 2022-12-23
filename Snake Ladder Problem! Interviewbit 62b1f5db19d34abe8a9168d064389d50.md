# Snake Ladder Problem! | Interviewbit

Created: July 26, 2022 1:16 PM
Tags: BFS, Graphs
URL: https://www.interviewbit.com/problems/snake-ladder-problem/

**Problem Description**

Rishabh takes out his **[Snakes and Ladders Game](https://en.wikipedia.org/wiki/Snakes_and_Ladders)**, stares the board and wonders: "If I can always roll the die to whatever number I want, what would be the **least number of rolls to reach the destination**?"

**RULES:**

- The game is played with cubic dice of **6** faces numbered from **1** to **A**.
- Starting from **1** , land on square **100** with the exact roll of the die. If moving the number rolled would place the player beyond square **100**, no move is made.
- If a player lands at the base of a ladder, the player must climb the ladder. Ladders go up only.
- If a player lands at the mouth of a snake, the player must go down the snake and come out through the tail. Snakes go down only.

**BOARD DESCRIPTION:**

- The board is always `10 x 10` with squares numbered from **1** to **100**.
- The board contains **N** ladders given in a form of 2D matrix **A** of size `N * 2` where **(A[i][0], A[i][1])** denotes a ladder that has its base on square **A[i][0]** and end at square **A[i][1]**.
- The board contains **M** snakes given in a form of 2D matrix **B** of size `M * 2` where **(B[i][0], B[i][1])** denotes a snake that has its mouth on square **B[i][0]** and tail at square **B[i][1]**.

**Problem Constraints**

1 <= N, M <= 15

1 <= A[i][0], A[i][1], B[i][0], B[i][1] <= 100

A[i][0] < A[i][1] and B[i][0] > B[i][1]

Neither square **1** nor square **100** will be the starting point of a ladder or snake.

A square will have at most one endpoint from either a snake or a ladder.

**Input Format**

First argument is a 2D matrix **A** of size `N * 2` where **(A[i][0], A[i][1])** denotes a ladder that has its base on square **A[i][0]** and end at square **A[i][1]**.

Second argument is a 2D matrix **B** of size `M * 2` where **(B[i][0], B[i][1])** denotes a snake that has its mouth on square **B[i][0]** and tail at square **B[i][1]**.

**Output Format**

Return the **least number of rolls** to move from start to finish on a separate line. If there is no solution, return **-1**.

**Example Input**

Input 1:

```
 A = [  [32, 62]
        [42, 68]
        [12, 98]
     ]
 B = [  [95, 13]
        [97, 25]
        [93, 37]
        [79, 27]
        [75, 19]
        [49, 47]
        [67, 17]

```

Input 2:

```
 A = [  [8, 52]
        [6, 80]
        [26, 42]
        [2, 72]
     ]
 B = [  [51, 19]
        [39, 11]
        [37, 29]
        [81, 3]
        [59, 5]
        [79, 23]
        [53, 7]
        [43, 33]
        [77, 21]

```

**Example Output**

**Example Explanation**

Explanation 1:

```
 The player can roll a5 and a6 to land at square12. There is a ladder to square98. A roll of2 ends the traverse in3 rolls.

```

Explanation 2:

```
 The player first rolls5 and climbs the ladder to square80. Three rolls of6 get to square98.
 A final roll of2 lands on the target square in5 total rolls.

```

```cpp
int Solution::snakeLadder(vector<vector<int> > &A, vector<vector<int> > &B) {

        int N = A.size(), M = B.size();

        unordered_map<int, int> m;

        int count = 0;// bottom left number -> top right number on board

        bool flag = true;// bool for alternate traversal of rows

        

        // Store all the possible moves using snake and ladders in a map

        for(int i = 0; i < N; i++)

        m[A[i][0]] = A[i][1];

        for(int j = 0; j < M; j++)

        m[B[j][0]] = B[j][1];

        

        // Maintain queue for BFS

        queue<int> q;

        

        // Maintain visited numbers

        unordered_set<int> visited;

        visited.insert(1);

        q.push(1);

        

        int moves = 0;

        flag = false;

        

        // BFS

        while(!q.empty())

        {

            int size = q.size();

            moves++;// Increase number of moves

            for(int i = 0; i < size; i++)

            {

                auto temp = q.front(); q.pop();

                if(temp == 100)// final position reached

                {

                    moves--;// final position is already reached hence remove the last unused move

                    flag = true; break;

                }

                

                // push all the reachable postions from current number in the queue

                for(int j = temp + 1; j <= min(temp + 6, 100); j++)

                {

                    // if there is a ladder or snake then directly push the number where it goes

                    if(m.find(j) != m.end())

                    {

                        if(visited.find(m[j]) == visited.end())

                        {

                            q.push(m[j]);

                            visited.insert(m[j]);

                        }

                    }

                    // else push the 1 to 6 move with dice

                    else if(visited.find(j) == visited.end())

                    {

                        q.push(j);

                        visited.insert(j);

                    }

                }

            }

            if(flag)break;

        }

        return (flag)?moves:-1;// flag is true only when final position is reached 

}
```