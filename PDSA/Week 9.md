- **Dynamic Programming:** It says that whenever I see a problem then I will already have a solution ready for it. It is *Bottom Up*.
- **Memoization:** It says that whenever we see a solution, we will memorize it to make use of it in future. It is *Top Down*.
- For dynamic programming we need to take care of two things:
		- Recursive case(s)
		- Base case(s)

#### Properties of Dynamic Programming

- Overlapping sub problem
- The solution of the sub problem must contribute to the solution of the larger problem.

# Grid Paths

> Only Upward and Right turns are **allowed**
> Downward and Left turns are **not allowed**

- **Number of ways to reach point (m,n) from (0,0):** $_{m+n} C _n$ or $_{m+n} C _m$
- If there is *a* point (a,b) that we need to avoid then:
	- We will track all ways to reach to (a,b): $_{a+b} C_a$
	- Track all ways to reach to actual point (m,n) by considering (a,b) as origin: $_{(m-a)+(n-b)} C_{(m-a)}$ 
	- Multiply them both since they are *independent*
	- Then subtract the result from the actual number of ways to reach to (m,n) from the actual origin: $_{m+n}C_m$
- If there are *two* points() then the situation becomes very complex so we will take a different approach.

- In the grid:
	- $W[i][j]$ = $W[i-1][j]$ + $W[i][j-1]$
	- Here, $i$ and $j$ are coordinates
	- The equation says that number of turns required to reach $(i,j)$ is summation of number of turns at the $(i-1, j)$ and $(i, j-1)$
	- To visualize this, check this diagram below.
	- Now we can put this in dynamic programming and solve the above issue.

#### Base cases

- There will be three base cases in this:
	- $W[0][0]$ = 1
	- $W[i][0]$ = 1
	- $W[0][j]$ = 1
 The base cases are taken because these do not have any dependency as compared to other coordinates.
- And wherever we see a blocked coordinate $(x,y)$:
	- $W[x][y]$ = 0

![[Grid Path.png]]


# Longest Common Substring

Let's say that there two words:
	1. Hello
	2. Fellow

- In the above two words the longest common substring is `ello`
- Our target is to find out the `k` which is the length of the longest common substring.

> There are two words $A$ and $B$ for which the indices are $i$ and $j$ respectively and have the length as $M$ and $N$ respectively.

- In this implementation we will consider that when we say `i` then it means that we're considering from index `i` to the last index `m` of the said word.
- In $LCS[i,j]$
	- $i$ is from the first word $A$
	- $j$ is from the second word $B$
- If both $i^{th}$ and $j^{th}$ index of the respective words have *same character*
	- $LCS[i,j]$ = $LCS[i+1, j+1] + 1$
- If both $i^{th}$ and $j^{th}$ index of their respective words have *different character*
	- $LCS[i,j]$ = 0

#### Base cases

- $LCS[M,N] = 0$ ; both indices are at the end
- $LCS[M,j] = 0$ ; one index is at the end
- $LCS[i,N] = 0$ ; one index is at the end

![[Longest Common Substring.png]]

#### How to put in in dynamic programming

- Let's put the above equation in matrix form:
	- $LCS[i][j]$ = $LCS[i+1][j+1]$ + 1
- From the above equation it is clear that to find $(i,j)$ we need to find out $(i+1, j+1)$, so the values are dependent on the values diagonally below it.
- So we will not start with the base cases and keep on building the matrix as in the figure above.

```Python
def LCW(u,v):
	import numpy as np
	(m,n) = (len(u), len(v))
	lcw = np.zeros((m+1, n+1))


	maxlcw = 0 

	for c in range(n-1, -1, -1):
		for r in range(m-1, -1, -1):
			if u[r] == v[c]:
				lcw[r,c] = 1 + lcw[r+1, c+1]
			else:
				lcw[r,c] = 0
			if lcw[r,c] > maxlcw:
				maxlcw = lcw[r,c]
	return(maxlcw)
```


# Longest Common Subsequence

- Difference between substring & subsequence is that substring has to be continuous whereas subsequence can be discontinuous but the order of alphabets has to be maintained.

- Everything is same as [[#Longest Common Substring]] the only difference is that as mentioned above that there can discontinuous but ordered alphabets here so we need to tweak out algorithm a little.

- Previously we put $LCS[i,j] = 0$ when $a_i \ne b_j$ 
- Now when this happens then instead of putting $0$ we will just move over to the next word to check if there are any more ordered alphabets.
- And since this can be done from both ways (for both words) so we will take the max of both ways and use it.
-  So now the equations stands as:
	- If both $i^{th}$ and $j^{th}$ index of the respective words have *same character*
		- $LCS[i,j]$ = $LCS[i+1, j+1] + 1$
	- If both $i^{th}$ and $j^{th}$ index of their respective words have *different character*
		- $LCS[i,j]$ = $max(LCS[i+1, j], LCS[i,j+1])$

- And since we tweaked the algorithm a little so now our value is not only dependent on the diagonally below value but also the value underneath and to the right.
- Imagine from origin $(0,0)$ and put it in the above two equations of $LCS$
- Refer to the diagram for more visualization.


![[Longest Common Subsequence.png]]

#### Base Cases
Same as [[#Base cases]]

```Python
def LCS(u,v):
	import numpy as np
	(m,n) = (len(u), len(v))
	lcs = np.zeros((m+1, n+1))

	for c in range(n-1, -1, -1):
		for r in range(m-1, -1, -1):
			if u[r] == v[c]:
				lcs[r,c] = 1 + lcs[r+1, c+1]
			else:
				lcs[r,c] = max(lcs[r+1,c], lcs[r, c+1])
	return(lcs[0,0])
```


# Edit Distance

