# Union-Find Structure

- **MakeUnionFind(s)** initializes all vertices into singleton.
- **Find(u)** will search for vertex `u` in all partition and tells us which partition it is.
- **Union(u,v)** will take the partition of `u` and `v` and merge them into a single partition.

#### Summary
- We can implement Union-Find using arrays/dictionaries `Component`, `Members`, `Size`.
	- `MakeUnionFind(s)` is $O(n)$
	- `Find(i)` is $O(1)$
	- `Union(i,j)` is $O(n)$
	- Sequence of `m` union operations takes time $O(mn)$

```Python
class MakeUnionFind:
	def __init__(self):
		self.component = {}
		self.members = {}
		self.size = {}

	def make_union_find(self, vertices):
		for vertex in range(vertices):
			self.components[vertex] = vertex
			self.members[vertex] = [vertex]
			self.size[vertex] = 1

	def find(self, vertex):
		return self.components[vertex]

	def union(self, u, v):
		c_old = self.components[u]
		c_new = self.components[v]

		# Alwasys add member in components which have greater size
		if self.sixe[c_new] >= self.size[c_old]:
			for x in self.members[c_old]:
				self.components[x] = c_new
				self.members[c_new].append(x)
				self.size[c_new] += 1
		else:
			for x in self.members[c_new]:
				self.components[x] = c_old
				self.members[c_old].append(x)
				self.size[c_old] += 1
				
```

```Python
def kruskal(WList):
	(edges, TE) = ([], [])
	for u in WList.keys():
		edges.extend([(d,u,v) for (v,d) in WList[u]])
	edges.sort()

	mf = MakeUnionFind()
	mf.make_union_find(len(WList))
	for (d,u,v) in edges:
		if mf.components[u] != mf.components[v]:
			mf.union(u,v)
			TE.append((u,v,d))
		# We can stop the process if the size becomes equal to the total number of edges
		# Which represent that a spanning tree is completed

		if mf.size[mf.components[u]] >= mf.size[mf.components[v]]:
			if mf.size[mf.components[u]] == len(Wlist);
				break
		else:
			if mf.size[mf.components[v]] == len(WList):
				break

	return(TE)
	
	
# Testcase

edge = [(0,1,10),(0,2,18),(0,3,6),(0,4,20),(0,5,13),(1,2,10),(1,3,10),(1,4,5),(1,5,7),(2,3,2),(2,4,14),(2,5,15),(3,4,17),(3,5,12),(4,5,10)]

size = 6
WL = {}
for i in range(size):
    WL[i] = []
for (i,j,d) in edge:
    WL[i].append((j,d))
print(kruskal(WL))
```

```Output
[(2, 3, 2), (1, 4, 5), (0, 3, 6), (1, 5, 7), (0, 1, 10)]
```

##### Complexity
- Tree has $n-1$ edges, so $O(n)$ union() operations
- $O(n logn)$ amortized overall cost
- Sorting E takes $O(mlogm)$
	- Equivalently $O(m logn)$, since $m \le n^2$
- Overall time, $O(m + n) log n$ 

# Priority Queue

Need to maintain a collection of items with priorities to optimize the following operations
-   **delete max()**
    -   Identify and remove item with highest priority
    -   Need not be unique
-   **insert()**
    -   Add a new item to the list

# Heaps

- **Binary tree** has to be filled *top to bottom* and *left to right*.
- **Binary tree** is a data structure in which each node can contain at most 2 nodes.

- **Heaps** are two types:
	- *Max heap:* Where the parent node will have higher value than it's children.
	- *Min heap:* Where the parent node will have lower value than it's children.
- We will study about binary heap here which will have property of both binary tree and heap.
- Apart from that, binary heap will also have *No holes* property.

- We will represent binary heap in array/list
	- `H = [h0, h1, h2, h3, h4, h5, h6, h7, h8, h9]`
	- left child of `H[i] = H[2 * i + 1]`
	- Right child of `H[i] = H[2 * i + 2]`
	- Parent of `H[i] = H[(i-1) // 2], for i > 0`

```Python
class minheap:
	def __init__(self):
		self.A = []

	def min_heapify(self,k):
		l = 2 * k + 1
		r = 2 * k + 2
		smallest = k

		if l < len(self.A) and self.A[l] < self.A[smallest]:
			smallest = l
		if r < len(self.A) and self.A[r] < self.A[smallest]:
			smallest = r
		if smallest != k:
			self.A[k], self.A[smallest] = self.A[smallest], self.A[k]
			self.min_heapify(smallest)

	def build_min_heap(self, L):
		self.A = []
		for i in L:
			self.A.append(i)
		n = int((len(self.A)//2)-1)

		for k in range(n, -1, -1):
			self.min_heapify(k)


	def delete_min(self):
		item = None
		if self.A != []:
			self.A[0], self.A[-1] = self.A[-1], self.A[0]
			item = self.A.pop()
			self.min_heapify(0)
		return item

	def insert_in_minheap(self, d):
		self.A.append(d)
		index = len(self.A) - 1
		while index > 0:
			parent = (index - 1)//2
			if self.A[index] < self.A[parent]:
				self.A[index], self.A[parent] = self.A[parent], self.A[index]
				index = parent
			else:
				break


heap = minheap()
heap.build_min_heap([6,5,4,3,2])
print(heap.A)
heap.insert_in_minheap(1)
print(heap.A)
heap.insert_in_minheap(8)
print(heap.A)
print(heap.delete_min())
print(heap.delete_min())
print(heap.A)
```

```Output
[2, 3, 4, 6, 5]
[1, 3, 2, 6, 5, 4]
[1, 3, 2, 6, 5, 4, 8]
1
2
[3, 5, 4, 6, 8]
```

##### Complexity
Heaps are a tree implementation of priority queues

-   `insert()` is $O(N)$
-   `delete max()` is $O(logN)$
-   `heapify()` builds a heap in $O(N)$

# Improve Dijkstra's algorithm using min heap

#### Using adjacency list

```Python
def min_heapify(i,size):
    lchild = 2*i + 1
    rchild = 2*i + 2
    small = i
    if lchild < size-1 and HtoV[lchild][1] < HtoV[small][1]: 
        small = lchild
    if rchild < size-1 and HtoV[rchild][1] < HtoV[small][1]: 
        small = rchild
    if small != i:
        VtoH[HtoV[small][0]] = i
        VtoH[HtoV[i][0]] = small
        (HtoV[small],HtoV[i]) = (HtoV[i], HtoV[small])
        min_heapify(small,size)

def create_minheap(size):
    for x in range((size//2)-1,-1,-1):
        min_heapify(x,size)

def minheap_update(i,size):
    if i!= 0:
        while i > 0:
            parent = (i-1)//2
            if HtoV[parent][1] >  HtoV[i][1]:
                VtoH[HtoV[parent][0]] = i
                VtoH[HtoV[i][0]] = parent
                (HtoV[parent],HtoV[i]) = (HtoV[i], HtoV[parent])
            else:
                break
            i = parent

def delete_min(hsize):
    VtoH[HtoV[0][0]] = hsize-1
    VtoH[HtoV[hsize-1][0]] = 0
    HtoV[hsize-1],HtoV[0] = HtoV[0],HtoV[hsize-1]  
    node,dist = HtoV[hsize-1]
    hsize = hsize - 1
    min_heapify(0,hsize) 
    return node,dist,hsize


HtoV, VtoH = {},{}
#global HtoV map heap index to (vertex,distance from source)
#global VtoH map vertex to heap index
def dijkstralist(WList,s):
    infinity = float('inf')
    visited = {}
    heapsize = len(WList)
    for v in WList.keys():
        VtoH[v]=v
        HtoV[v]=[v,infinity]
        visited[v] = False
    HtoV[s]= [s,0]
    create_minheap(heapsize)
    
    for u in WList.keys():
        nextd,ds,heapsize = delete_min(heapsize)             
        visited[nextd] = True        
        for v,d in WList[nextd]:
            if not visited[v]:
                HtoV[VtoH[v]][1] = min(HtoV[VtoH[v]][1],ds+d)
                minheap_update(VtoH[v],heapsize)


dedges = [(0,1,10),(0,2,80),(1,2,6),(1,4,20),(2,3,70),(4,5,50),(4,6,5),(5,6,10)]
#edges = dedges + [(j,i,w) for (i,j,w) in dedges]
size = 7
WL = {}
for i in range(size):
    WL[i] = []
for (i,j,d) in dedges:
    WL[i].append((j,d))
s = 0
dijkstralist(WL,s)
#print(HtoV)
#print(VtoH)
for i in range(size):
    print('Shortest distance from {0} to {1} = {2}'.format(s,i,HtoV[VtoH[i]][1]))
```

#### Code summary

This is an implementation of Dijkstra's algorithm using adjacency list and min-heap data structure for efficient processing of the next minimum element in the list. Here's how the code works:

1.  `min_heapify`: This function is used to maintain the min-heap property of the heap. Given an index `i` and heap size `size`, it checks if the left child and right child of the current node (`i`) satisfy the min-heap property or not. If not, it swaps the current node with the smallest child and recursively calls the function on the new child node, until the min-heap property is satisfied.
    
2.  `create_minheap`: This function is used to create a min-heap from the given heap size `size`. It starts from the middle of the heap and calls `min_heapify` on each node, moving towards the root of the heap.
    
3.  `minheap_update`: This function updates the min-heap property by moving an element up the heap if it violates the property. It takes an index `i` and heap size `size` as input and repeatedly swaps the element with its parent if its parent is greater than the element, until the heap property is satisfied.
    
4.  `delete_min`: This function removes the minimum element from the heap and returns it. It takes the heap size `hsize` as input, removes the first element (the minimum) and places the last element at the first position. Then, it calls `min_heapify` to maintain the min-heap property.
    
5.  `dijkstralist`: This function is the main function that performs Dijkstra's algorithm on a given weighted adjacency list `WList` starting from a source node `s`. It initializes the heap with all vertices with distance set to infinity, except the source vertex with distance 0. Then, it repeatedly extracts the minimum element from the heap and visits its neighbors, updating their distance if a shorter path is found. It uses the `minheap_update` function to maintain the heap property when updating distances.

At the end of the algorithm, `HtoV` stores the shortest distance from the source to each vertex, and `VtoH` maps each vertex to its corresponding index in the heap. The code then prints the shortest distance from the source to each vertex.


# Binary Search Tree

- Used for **dynamic** storing of data
- Following are the properties of a BST:
	- The value of the left child is always less than the value of v.
	- The value of the right child is always greater than the value of v.
- Traversals:
	- Let's say `1` is the left child or lower child
	- `2` is the root child or mid child
	- `3` is the right child or higher child
	- Then
		- `[1,2,3]` is *in-order traversal*
		- `[1,3,2]` is *post-order traversal*
		- `[2,1,3]` is *pre-order traversal*

```Python
class Tree:
	# constructor
	def __init__(self. initval = None):
		self.value = initval
		if self.value:
			self.left = Tree()
			self.right = Tree()
		else:
			self.left = None
			self.right = None
		return

	# only empty node has value none
	def isempty(self):
		return (self.value == None)


	# leaf nodes have both children empty
	def isleaf(self):
		return (self.value != None and self.left.isempty() and self.right.isempty())


	# inorder traversal
	def inorder(self):
		if self.isempty():
			return([])
		else:
			return(self.left.inorder() + [self.value] + self.right.inorder())


	# display tree as a string
	def __str__(self):
		return(str(self.inorder()))


	# check if value v occurs in tree
	def find(self, v):
		if self.isempty():
			return(False)
		if self.value == v:
			return(True)
		if v < self.value:
			return(self.left.find(v))
		if v > self.value:
			return(self.right.find(v))


	# return minimum value for tree rooted on self - Minimum is left most node in the tree
	def minval(self):
		if self.left.isempty():
			return(self.value)
		else:
			return(self.left.minval())


	# return maximum value for tree rooted in self - Maximum value is the right most node in the tree
	def maxval(self):
		if self.right.isempty():
			return(self.value)
		else:
			return(self.right.maxval())


	# insert new element in binary search tree
	def insert(self, v):
		if self.isempty():
			self.value = v
			self.left = Tree()
			self.right = Tree()

		if self.value == v:
			return

		if v < self.value:
			self.left.insert(v)
			return

		if v > self.value:
			self.right.insert(v)
			return


	# delete element from binary tree
	def delete(self,v):
		if self.isempty():
			return

		if v < self.value:
			self.left.delete()
			return
		if v > self.value:
			self.right.delete()
			return

		if v == self.value:
			if self.isleaf():
				self.makeempty()
			elif self.left.isempty():
				self.copyright()
			elif self.right.isempty():
				self.copyleft()

			else:
				self.value = self.left.maxval()
				self.left.delete(self.left.maxval())
			return


	# convert leaf node to empty node
	def makeempty(self):
		self.value = None
		self.left = None
		self.right = None
		return


	# promote left child
	def copyleft(self):
		self.value = None
		self.right = self.left.right
		self.left = self.left.left
		return

	def copyright(self):
		self.value = None
		self.left = self.right.left
		self.right = self.right.right
		return

T = Tree()
bst = [9,8,7,6,5,4,3,2,1]
k = 4
for i in bst:
    T.insert(i)
print('Element in BST are:= ',T.inorder())
print('Maximum element in BST are:= ',T.maxval())
print('Minimum element in BST are:= ',T.minval())
print(k,'is present or not = ',T.find(k))
T.delete(3)
print('Element in BST after delete 3:= ',T.inorder())
```

```Output
Element in BST are:=  [1, 2, 3, 4, 5, 6, 7, 8, 9]
Maximum element in BST are:=  9
Minimum element in BST are:=  1
4 is present or not =  True
Element in BST after delete 3:=  [1, 2, 4, 5, 6, 7, 8, 9]
```

##### Complexity
-   `find()`, `insert()` and `delete()` all walk down a single path
-   Worst-case: height of the tree
-   An unbalanced tree with n nodes may have height $O(n)$
-   Balanced trees have height $O(logn)$
-   Will see how to keep a tree balanced to ensure all operations remain $O(logn)$