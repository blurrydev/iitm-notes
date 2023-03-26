# Divide and Conquer - Counting  Inversions

#### Recommender System

Suppose there are movies `A B C D E`
So me and my friends are to rate this movies from 1 to 5

Let's say my ratings are `D A C B E`
My friend's ratings are `A E D C B`

Now we compare pairs and see the preference. Example: `A C`, both me and my friend prefer movie `A` more than movie `C`.

But when it comes to `B E`, I like movie `B` more than movie `E` but my friend likes the exact *opposite*. This is called an **Inversion**.

##### Inversions
In a list of `n` 

Inversions can range from:
- `0` : There are no inversions so the rankings are *identical*.
- `n(n-1)/2` : Every pair is inverted so the rankings are *complete opposite*.

#### Algorithm

The inversion count is a measure of how far an array is from being sorted. It is defined as the number of pairs of elements that are out of order in the array. For example, in the array [2,4,3,1,5], there are three inversions: (4,3), (4,1), and (3,1).

1.  The inversion count is the number of pairs of elements that are out of order in an array.
2.  The algorithm uses a divide and conquer approach to count inversions.
3.  It recursively splits the input array into two halves until the base case of an array of length 1 is reached.
4.  It counts the inversions in each half and also counts the inversions between the two halves.
5.  It merges the two halves and returns the sorted array and the total number of inversions.
6.  The final output is the total number of inversions in the original input array.
7. **Time Complexity:** $2T(n/2) + n =$ $O(n*logn)$ 

```Python
global count

def mergeAndCount(A,B):
	(m,n) = (len(A), len(B))
	(C, i, j, k) = ([],0,0,0)

	while k < m+n: # While not all elements have been processed
		if i == m: # If all elements in list A have been processed
			C.append(B[j]) # Add the remaining elements in list B to list C
			j += 1
			k += 1
		
		elif j == n: # If all elements in list B have been processed
			C.append(A[i]) # Add the remaining elements in list A to list C
			i += 1
			k += 1
			
		elif A[i] < B[j]: # If the current element in list A is less than the current element in list B
			C.append(A[i])
			i += 1
			
		else: # If the current element in list B is less than or equal to the current element in list A
			C.append(B[j])
			j += 1
			count += m-i # Increment the count by the number of elements remaining in list A
		return C


count = 0
def inversionCount(A):
	n = len(A)
	if n <=1:
		return(A,0)

	(L) = inversionCount(A[:n//2])
	(R) = inversionCount(A[n//2:])
	(B) = mergeAndCount(L,R)
	return B


L = [2,4,3,1,5]
print(inversionCount(L))
print(count)
```

```Output
4 # 4 is the number of inversions
```

The given code implements a function called `inversionCount` that counts the number of inversions in an input array. An inversion occurs when two elements in the array are not in sorted order.

The code uses a divide-and-conquer approach to recursively divide the input array into smaller subarrays until the subarrays contain only one or zero elements. The subarrays are then merged using the `mergeAndCount` function, which counts the number of inversions between the two subarrays.

The `mergeAndCount` function works by iterating over the elements in the two subarrays and appending them to a new array in sorted order. Whenever an element from the second subarray is appended to the new array before an element from the first subarray, the count variable is incremented by the number of remaining elements in the first subarray.

The final count of inversions is returned by the `inversionCount` function, which sums the counts of inversions from each recursive call to `mergeAndCount`. The code also prints the count of inversions in the input array.

# Closest Pair of Points

- Several objects on the screen
- **Naïve algorithm** will find the distance between all the points and then return the points with the minimum distance which will take $O(n^2)$.
- **Clever algorithm** will take $O(n*logn)$ using divide and conquer.

#### Algorithm
- Given n points $p1, p2, ..., pn$ find the closest pair.
	1. Assume no two points have same $x$ and $y$ components.
	2. Split the points into two halves by a vertical line.
	3. Recursively compute the closest pair in each half
	4. Compare the shortest distance in each half to the shortest distance across the dividing line.

#### Logic
- If we have two points then we will directly return the distance.
- If we have three points then we will directly return the minimum distance.
- If we have more than three points we will divide the space into two halves and keep dividing it until we have 2 or three points in the space, for each space. 
	- For the spaces with 2 or 3 points can be solved using the base case.
- From each space we will get a minimum distance. We will compare all of them and find the minimum of the minimum distance.
- Now we will also try to find smaller distance across the borders dividing the spaces. This is done so we can find the smallest cross border distance and compare it with the within space distance to find the actual minimum distance.

 ##### How to find the cross border minimum distance
 

```Python
import math

# return euclidean distance between points p and q
def distance(p,q):
	return math.sqrt(math.pow(p[0] - q[0], 2) + math.pow(p[1] - q[1], 2))

# Recursive function to find the closest pair of points
def minDistanceRec(Px, Py):
	s = len(Px)

	# if only 2 or 3 points are left then return minimum distance accordingly
	if s == 2:
		return distance(Px[0], Px[1])
	elif s == 3:
		return min(distance(Px[0], Px[1]), distance(Px[1], Px), distance(Px[2], Px[0]))



	# For more than 3 points divide the points by a vertical line passing through the median of the x-coordinates
	m = s //2
	Qx = Px[:m] # points on the left of the vertical
	Rx = Px[m:] # points on the right of the vertical
	xR = Rx[0][0] # minimum X coordinate on the right

	# Construct Qy and Ry by iterating all the points in py and adding them in Qy or Ry based on their x-coordinates
	Qy = []
	Ry = []
	for p in Py:
		if p[0] < xR:
			Qy.append(p)
		else:
			Ry.append(p)

	# Recursively compute the closest pair of points in each half
	delta = min(minDistanceRec(Qx, Qy), minDistanceRec(Rx, Ry))


	# Create Sy by selecting points from Py whose x-coordinates are within delta of xR.
	Sy = []
	for p in Py:
		if abs(p[0] - xR) <= delta:
			Sy.append(p)


	# Compare distance between all pairs of points in Sy and return the minimum distance.
	sizeS = len(Sy)
	if sizeS > 1:
		minS = distance(Sy[0], Sy[1])
		for i in range(1, sizeS - 1):
			# check only 15 points at a time to optimize the algorithm
			for j in range(i, min(i+15, sizeS-1)):
				minS = min(minS, distance(Sy[i], Sy[j+1]))
		return min(delta, minS)
	else:
		return delta

# Function to compute the closest pair of points
def minDistance(points):
	# sort the points by x-coordinates
	Px = sorted(points)
	# sort the points by y-coordinates
	Py = points
	Py.sort(key=lambda x: x[-1])
	return round(minDistanceRec(Px, Py), 2)


# Sample usage
pts = [(2, 15), (40, 5), (20, 1), (21, 14), (1, 4), (3, 11)]
result = minDistance(pts)
print(result)
```

```Output
4.12
```

# Multiplication: Karatsuba Algorithm

#### Karatsuba Algorithm

1.  Given two numbers x and y, we split them into two parts each, *a high part* and *a low part*. We do this by selecting a splitting point, which is usually the midpoint of the number with the most digits.

2.  We then recursively compute:
	1. The product of the high parts 
	2. The product of the low parts 
	3. The product of the sum of the high and low parts. This can be done by recursively applying the Karatsuba algorithm.

3.  We then combine the results of these three products using some simple arithmetic to get the final result.

#### Pseudo Code

```Python
Fast-Multiply(x, y, n):
	if n=1:
		return x * y
	else:
		m = n//2
	# divided by 2**m gives the first m nnumber of the orignal number
	# mod by 2**m gives the last m number of the original number
		(x_1, x_0) = (x/2**m, x mod 2**m) # bit shifting
		(y_1, y_0) = (y/2**m, y mod 2**m) # bit shifting
	# we took 2 because the numbers are binary, it can be changed accordingly
		(a, b) = (x_1 - x_0, y_1 - y_0)

		p = Fast-Multiply(x_1, y_1, m)
		q = Fast-Multiply(x_0, y_0, m)
		r = Fast-Multiply(x_1 - x_0, y_1 - y_0)


		return (p * 2**n) + ((p + q - r)* 2**(n/2)) + q
```

# Recursion Trees

Recursion trees are a useful tool for analyzing recursive algorithms. To create a recursion tree, you start with the initial input to the algorithm at the root of the tree, and then draw a child node for each recursive call made by the algorithm. Each level of the tree represents a new recursive call, and the depth of the tree corresponds to the number of times the recursive calls are made.

To analyze the time complexity of a recursive algorithm using a recursion tree, you need to determine how many leaves are in the tree (i.e., the number of base cases), and how much work is done at each level of the tree. You can then use this information to calculate the total amount of work done by the algorithm.

#### How to do it

1.  Draw a recursion tree representing the recursive calls made by the algorithm.
2.  Assign the amount of work done to each node in the tree (usually in terms of the size of the subproblem).
3.  Determine the number of nodes in the tree and the work done at each level of the tree.
4.  Use the following formula to express the time complexity in terms of work done:
    - *If the work done at each level is constant*, the time complexity is `O(work at the root * number of nodes in the tree)`.
    - *If the work done at each level is a constant factor smaller than the previous level*, the time complexity is `O(work at the leaves * number of leaves)`.
    - *If the work done at each level is a constant factor larger than the previous level*, the time complexity is `O(work at the root * number of nodes in the tree)`.


> The Master Theorem is a formula for solving a more general class of recurrence relations that arise in divide-and-conquer algorithms. It provides a way to determine the time complexity of an algorithm based on the size of the input and the amount of work done by the algorithm at each level of the recursion tree.


# Master's Theorem

If we can write the complexity of recursion relation as:

									$T(n) = aT(n/b) + f(n), a>=1, b>1$
									$T(n) = aT(n/b) + \Theta(n^c), a>=1, b>1$
 > $f(n) = \Theta(n^c)$
									
1. Find $log_b$ $a$
	- $log_b$ $​a$= $log_2$​ $a$ / $log_2$ $​b​$
2. Now compare it with:
	- If $c < log_b$ $a$, then $T(n) = O( n^{log_b a} )$
	- If $c == log_b$ $a$, then $T(n) = O(n^c log n)$
	- If $c > log_b$ $a$, then $T(n) = O(f(n))$

# Quick Select

#### Difference between normal quick sort and quick select

##### Quick Sort

```Python
l = pivot
quickSort(start, l, array)
quickSort(l+1, end, array)
```

##### Quick Select

- We're trying to find the $K^{th}$ smallest element in a list which is in descending order.
- There are three partitions:
	- Lower: Lower than pivot
	- Pivot
	- Upper: Higher than pivot

- Let `m = len(lower)`
	- `k <= m` then answer lies in `lower`, then `select(lower, k)`
	- `k = m+1` then answer is `pivot`, then `return(k)`
	- `k >= m+1` then answer lies in `upper`, then `select(upper, k - (m+1))`

###### Time complexity

$T(n)$ = $max(T(m), T(n - (m+1)))$ + $n$

Worst case: m is 0 or n-1, i.e terminal
Then, $T(n)$ becomes $O(n^2)$

In this method the complexity largely depends upon the pivot elements, we know this from `quickselect`. 

So we need an optimal algorithm to get the perfect pivot which will not be a terminal element, which is **Median of Median**.

# Median of Median

- Take an array and divide it into a sub arrays of 5 elements.
- Then sort of the sub arrays
- Take the median of each sub lists and create a new array with the medians.
- Now take the median of the array of medians
- Use it as the **Pivot**.

**Time Complexity:** $O(n)$

**Time complexity of QuickSelect with MoM:** $O(n)$
