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
def mergeAndCount(A,B):
	(m,n) = (len(A), len(B))
	(C, i, j, k, count) = ([],0,0,0,0)

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
		return(C,count)



def inversionCount(A):
	n = len(A)
	if n <=1:
		return(A,0)

	(L, countL) = inversionCount(A[:n//2])
	(R, countR) = inversionCount(A[n//2:])
	(B,countB) = mergeAndCount(L,R)
	return(B, countL + countR + countB)


L = [2,4,3,1,5]
print(inversionCount(L)[1])
```

```Output
4 # 4 is the number of inversions
```

The `inversionCount` function first checks if the length of the array is less than or equal to 1. If it is, there are no inversions, and so the function simply returns the original array and 0 (i.e., no inversions).

If the length of the array is greater than 1, the function divides the array into two halves `L` and `R` and recursively calls `inversionCount` on each half. This process continues until the length of the array is less than or equal to 1.

Once the recursive calls have returned the sorted subarrays `L` and `R` and the counts of their inversions, the function calls `mergeAndCount` to merge the two subarrays together while counting the number of inversions that cross over from one subarray to the other.

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
	xP = Rx[0][0] # minimum X coordinate on the right

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
