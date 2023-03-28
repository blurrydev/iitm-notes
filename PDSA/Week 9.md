- **Dynamic Programming:** It says that whenever I see a problem then I will already have a solution ready for it. It is *Bottom Up*.
- **Memoization:** It says that whenever we see a solution, we will memorize it to make use of it in future. It is *Top Down*.

#### Properties of Dynamic Programming

- Overlapping sub problem
- The solution of the sub problem must contribute to the solution of the larger problem.

# Grid Paths

- **Number of ways to reach point (m,n) from (0,0):** $_{m+n} C _n$ or $_{m+n} C _m$
- If there is *a* point (a,b) that we need to avoid then:
	- We will track all ways to reach to (a,b): $_{a+b} C_a$
	- Track all ways to reach to actual point (m,n) by considering (a,b) as origin: $_{(m-a)+(n-b)} C_{(m-a)}$ 
	- Multiply them both since they are *independent*
	- Then subtract the result from the actual number of ways to reach to (m,n) from the actual origin: $_{m+n}C_m$
- If there are *two* points()