# Lecture 1: Analysis of Algorithms

### Order of magnitude

- **Asymptotic Complexity:** When *n* becomes large, which of the algorithms is going to perform better.

> When we keep dividing by 2 then the order of complexity is log n
> When we have nested loops, then for each loop we get n times more. (n, n^2 , n^3 ...)

#### Example 1: SIM cards vs Aadhaar Cards

- $n$ $\approx$ $10^9$ - number of cards
- Naive algorithm: $t(n)$ $\approx$ $n^2$
- Clever algorithm: $t(n)$ $\approx$ n log $n$
	- log $n$ - number of times you need to divide n by 2 to reach 1
	- log n = k $\Rightarrow$ n = $2^k$

## Summary
- Two important parameters when measuring algorithm performance:
	- Running time
	- Memory Requirement (space)
- We will focus mainly on *running time*
- Running time *t(n)* is a function of input size *n*
	- Interested in order of magnitude
	- Asymptotic complexity, as *n* becomes large.
- From running time we estimate feasible input size
- We focus on worst case inputs:
	- Pessimistic, but easier to calculate than average case.
	- Upper bound on worst case gives us an overall guarantee on performance.

# Lecture 2: Comparing orders of magnitude

- Each of the lower curves of the complexity will be the big O of the upper curve

### Upper bounds

- For formally proving that something is big O we need to demonstrate the constants $c$ and $x_0$

 #### Example 1
 
 - 100n + 5 is $O(n^2)$
We need to manipulate this and get the $c$ and $x_0$

- 100n + 5 <= 100n + n for n > 5
- 100 n + n = 101n
- 101n <= 101$n^2$ 
- So from here we can conclude that $n_0$ = 5 (because $n_0$ is the threshold) and $c$ = 101 (because 101$n^2$ is of the form $cn^2$)

The above basically says $\forall$ n >= $n_0$ (5), 100n + 5 <= 101 $n^2$

> we take c from the upper order of magnitude or the one from inside big O

#### Example 2

- 100$n^2$ + 20n + 5 is $O(n^2)$
	- 100$n^2$ + 20n + 5 = 100$n^2$ + 20$n^2$ + 5$n^2$ , for n >= 1
	- 100$n^2$ + 20$n$ + 5 = 125$n^2$ , for n >= 1
	- So, $n_0$ = 1, $c$ = 125

#### Useful Properties
- When we have a two or more functions then we will consider the highest time complexity as the complexity of the whole thing.

### Lower Bounds
- We use lower bounds to say that to perform some operations we need *at-least* this much time.
For example:
	- $n^3$ is $\Omega$$(n^2)$

We typically establish lower bound for a problem rather than an algorithm.
- If we sort a list comparing elements and swapping them, we require $\Omega$(n log n) comparisons.
- This is independent of the algorithm we use for sorting.

### Tight Bound

- $f(x)$ is said to be $\Theta$$(g(x))$ if it is both $O(g(x))$ and $\Omega$$(g(x))$
	- Find constants $c_1$ , $c_2$ , $x_0$ such that $c_1$g(x) $\leq$ f(x) $\leq$ $c_2$g(x) for every x $\geq$ $x_0$

# Lecture 3: Calculating Complexity

Demonstration on how to calculate time complexity.

# Lecture 4: Searching in a List

#### Naïve Search

^83f669

- Search in an unsorted list takes time *O(n)*

```python 
def naivesearch(v,l):
	for x in l:
		if v == x:
			return True
	return False
```

- Need to scan the entire list.
- Worst case when value is not present.

#### Binary Search

^5b7ed4

- For a sorted list *Binary search takes time O(log n)*

```python
def binarysearch(v,l):
	if l == []:
		return False

	m = len(l) // 2
	if v == l[m]:
		return True
	
	if v < l[m]:
		return(binarysearch(v, l[:m]))
	else:
		return(binarysearch(v, l[m+1:]))
```

- Halve the interval to search each time.
- Why O(log(n))?
	- In the first step list in n
	- In the next step list is n/2
	- In the next step list is n/4
	- And so on... Which is the pattern for log n.

# Lecture 5: Selection Sort

^46e713

- Selection sort is an intuitive algorithm to sort list.
- Repeatedly find the minimum ( or maximum) and append to sorted list.
- Worst case complexity is $O(n^2)$
	- Every input takes the same time since the inner loop will iterate through all the values regardless of the value, so no added advantage.

```python
def selection_sort(arr): 
	for i in range(len(arr)): 
		min_idx = i 
		for j in range(i+1, len(arr)): 
			if arr[j] < arr[min_idx]: 
				min_idx = j arr[i], arr[min_idx] = arr[min_idx], arr[i] return arr
```

>In this code, the outer loop iterates through all the elements in the list and the inner loop finds the minimum element from the unsorted part of the list. The minimum element is then swapped with the first element of the unsorted part. The process is repeated until the entire list is sorted.


# Lecture 6: Insertion Sort

^5a4be1

- Insertion sort is another intuitive algorithm to sort a list.
- Create a new sorted list
- Repeatedly insert elements into the sorted list
- Worst case complexity is $O(n^2)$
	- Unlike selection sort, not all cases takes time $n^2$
	- If list is already sorted, *Insert* stops in 1 step.
	- Overall time can be close to $O(n)$

#### Code

There are two ways to write insertion sort:
1. Iterative way

```python
def insertion_sort(l):

	n = len(l)
	if n < 1:
		return l
		
	for i in range(len(l)):
		current_value = l[i]
		position = i
		
		while position > 0 and l[position - 1] > current_value;
			(l[position], l[position - 1]) = (l[position - 1], l[position])
			position -= 1
	
	return l
```

2. Recursive way

```python
def Insert(l, v);
	n = len(l)
	if n == 0: # case 1 when the list is empty
		return [v]
	if v >= l[-1]: # case 2 when the last value of the list is smaller than the given value
		return l + [v]
	else:
		return Insert(l[:-1], v) + l[-1]

def ISort(l):
	n = len(l)
	if n < 1:
		return L
	l = Insert(Isort(l[:-1]), l[-1])
	return l
```


# Lecture 7: Merge Sort

^756b56

- Merge sort uses divide and conquer to sort list.
- Divide the list into two halves
- Sort each half
- Merge the sorted halves.

#### Code

```python
def merge(A,B):
	(m,n) = (len(A), len(B))
	(C,i,j) = ([],0,0)

	#Case 1: When both lists A and B have elements for comparing
	while i < m and j < n:
		if A[i] <= B[j]:
			C.append(A[i])
			i += 1
		else:
			C.append(B[j])
			j += 1

	#Case 2: If list B is over, shift all elements of A to C
	while i < m:
		C.append(A[i])
		i += 1

	#Case 3: If list A is over, shift all elements of B to C
	while j < n:
		C.append(B[j])
		j += 1
	
	# Return sorted merged list
	return C


# Recursively divide the problem into sub-problems to sort the input list L
def mergesort(L):
	n = len(L)
	if n <= 1:
		return L

	left_half = mergesort(L[:n//2])
	right_half = mergesort(L[n//2:])

	sorted_merge_list = merge(left_half, right_half) # <erge two sorted list left_half and right_haf
	return sorted_merge_list
```

# Lecture 8: Analysis of Merge Sort

- Merge sort takes time $O$(n log n)
- Variations are possible:
	- Union of two two sorted lists - *discard duplicates*, if `A[i] == B[j]`, move one copy to `C` and increment both `i` and `j`.
	- Intersection of two sorted lists - when `A[i] == B[j]`, move one copy to `C` otherwise discard the smaller of `A[i]`, `B[j]`
	- List difference - elements in `A` but not in `B`

- Disadvantage is that merge needs to create a new list to hold the merged elements.
- It is inherently recursive.

# Lecture 9: Implementation of Searching and Sorting algorithms

- Practical session on google colab