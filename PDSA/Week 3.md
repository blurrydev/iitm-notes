# Lecture 1: Quick Sort

^d3d8fe

- Quick sort uses divide and conquer like merge sort.
- By partitioning the list carefully, we avoid the merge step which allows in place sort.
- We can also have an iterative implementation to avoid cost of recursion.

#### Short comings of merge sort

- Merge needs to create a new list to hold merged elements
- Inherently recursive

```python
def quicksort(L, l, r):    # Sort list L from index l to r
	if (r-l <= 1):
		return L
	(pivot, lower, upper) = (L[l], l+1, l+1)
	for i in range(l+1, r):
		if L[i] > pivot:    # If the selected item is greater than pivot
			upper = upper + 1    # Extend upper
		else:
			(L[i], L[lower]) = (L[lower], L[i])    # swap L[i] with the start of upper segment.
			(lower, upper) = (lower+1, upper+1)    # shift both segments b 1
	# Now swap the pivot with the last element of lower to put it in middle
	(L[l], L[lower-1]) = (L[lower-1], L[l])
	lower = lower - 1    # shift lower by -1 since we put pivot in between

	# Recursive Calls
	quicksort(L, l, lower)    # Now sort the lower part using quick sort
	quicksort(L, lower+1, upper)    # Now sort the upper part using quick sort
	return(L)
```

# Lecture 2: Analysis of Quick Sort

- The worst case complexity of quicksort is $O(n^2)$
- The average case time complexity is $O$(n log n)
- Randomly choosing the pivot is a good strategy to beat worst case inputs
- Quick sort works inplace and can be implemented iteratively.
- Very fast in practice and often used in built in sort functions.

# Lecture 4: Concluding remarks on sorting algorithms

#### Stable sorting
Stability is when sorting does not affect the original sequence when two values are same

- Quick sort is not stable
-  Merge sort is stable if we merge carefully
	- Do not allow elements from left to overtake the elements from right

#### Best sorting algorithm
- Quick sort is often algorithm of choice despite $O(n^2)$ worst case scenario.
- Merge sort is typically used for external sorting.
- Other $O$(n log n) algorithm include *heap sort*
- Sometimes hybrid strategies are used.

# Lecture 5: Difference between lists and arrays (Theory)

- Sequences can be stored as lists or arrays
- Lists are flexible but accessing an element is $O(n)$
- Arrays support random access but are difficult to expand.
- Algorithm analysis needs to take into account the underlying implementation.

# Lecture 6: Designing a flexible list and operations on the same

#### Implementing lists in Python

- Python class `Node`
- A list is a sequence of nodes
	- `self.value` is the stored value
	- `self.next` points to the next node
- When `self.value` is `None` then the list is empty.
- `l1 = Node()` - Empty list
- `l2 = Node(5)` - Singleton list

```Python
class Node:
	def __init__(self, v = None):
		self.value = v
		self.next = None
		return
	def isempty(self):
		if self.value == None:
			return True
		else:
			return False
```

#### Appending to a list

- Add `v` to the end of the list `l`
- If `l` is empty, update `l.value` from `None` to `v`
- If at last value, `l.next` is `None`:
	- Point `next` at a new node with value `v`
- Otherwise recursively append to the rest of the list.

- Iterative implementation:
	- If empty, replace `l.value` by `v`
	- Loop through `l.next` to end of list
	- Add `v` to the end of the list.

```Python
def appendi(self,v):
	# append, iterative
	if self.isempty():
		self.value = v
		return
	temp = self
	while temp.next != None:
		temp = temp.next
	temp.next = Node(v)
	return
```

#### Inserting to a list

- Want to insert `v` at head
- Create a new node with `v`
- *Cannot change where head points*
- Exchange the values $v_0$ (where head is initially pointing) and `v`
- Make a new node point to `head.next`
- make `head.next` point to new node.

```Python
def insert(self, v):
	if self.isempty():
		self.value = v
		return
	newnode = Node(v)

	# Exchange values in self and newnode
	(self.value, newnode.value) = (newnode.value, self.value)

	# Switch links
	(self.next, newnode.next) = (newnode, self.next)

	return
```


#### Deleting a value v

- Remove the first occurrence of `v`
- Scan list for first `v` - look ahead at next node
- If next node value is `v`, bypass it
- *Cannot* bypass the first node in the list
	- Instead copy the second node value to head
	- Bypass second node
- Recursive implementation

```Python
def delete(self, v):
# delete recursive

	if self.isempty():
		return
	if self.value == v:
		self.value = None
		if self.next != None:
			self.value = self.next.value
			self.next = self.next.next
		return
	else:
		if self.next != None:
			self.next.delete(v)
			if self.next.value == None:
				self.next = None
	return
```


# Lecture 7: Implementation of Lists in Python

- Python lists are *not* implemented as flexible linked structures.
- Python allocates an array when we initiate a list and then doubles the space as needed.
- **Append, Pop** are cheap $O(1)$, **Insert, Delete** is expensive $O(n)$.
- Arrays can be represented as multidimensional lists, but *mutability, aliasing* is an issue.
- Numpy arrays are easier to use.

