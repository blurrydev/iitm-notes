# Balanced Search Tree (AVL Tree)

#### Binary Search Tree
- `find()`, `insert()` & `delete()` all walk down a single path.
- Worst case: Height of the tree, an unbalanced tree with node n may have height $O(n)$.

#### Rotations

> - **A left rotation** involves moving a node from its current position to the left of its right child.
> - **A right rotation** is the opposite of a left rotation. It involves moving a node from its current position to the right of its left child.

We use 4 types of rotations:

1.  LL Rotation:
    - Occurs when the balance factor of a node is greater than 1 and its left child's balance factor is greater than or equal to 0.
    - The rotation involves a right rotation at the unbalanced node, with *the parent becoming the right child of the left child*.
    - **After the rotation**, the previous right child of the left child becomes the left child of the newly rotated node.

1.  RR Rotation:
    - Occurs when the balance factor of a node is less than -1 and its right child's balance factor is less than or equal to 0.
    - The rotation involves a left rotation at the unbalanced node, with *the parent becoming the left child of the right child*.
    - **After the rotation**, the previous left child of the right child becomes the right child of the newly rotated node.

2.  LR Rotation:
    - Occurs when the balance factor of a node is greater than 1 and its left child's balance factor is less than 0.
    - The rotation involves *a left rotation at the left child*, followed by *a right rotation at the unbalanced node*, with the left child becoming the left child of the right child.
    - **After the rotation**, the previous right child of the left child becomes the left child of the newly rotated node, and the previous left child of the right child becomes the right child of the newly rotated node.

3.  RL Rotation:
    - Occurs when the balance factor of a node is less than -1 and its right child's balance factor is greater than 0.
    - The rotation involves *a right rotation at the right child*, followed by *a left rotation at the unbalanced node*, with the right child becoming the right child of the left child.
    - **After the rotation**, the previous left child of the right child becomes the right child of the newly rotated node, and the previous right child of the left child becomes the left child of the newly rotated node.


#### AVL Tree
- Balanced trees have height $O(logn)$.
- Using rotations we can balance a tree.
- Minimum number of trees: $S(h) = S(h-2) + S(h-1) + 1$
- Maximum number of trees: $2^h - 1$

#### Code
```Python
class AVLTree:
	# Constructor
	def __init__(self, initval=None):
		self.value = initval
		if self.value:
			self.left = AVLTree()
			self.right = AVLTree()
			self.height = 1
		else:
			self.left = None
			self.right = None
			self.height = 0
		return

	def isempty(self):
		return (self.value == None)

	def isleaf(self):
		return (self.value != None and self.left.isempty() and self.right.isempty())

	def leftrotate(self):
		v = self.value
		vr = self.right.value
		tl = self.left
		trl = self.right.left
		trr = self.right.right

		newleft = AVLTree(v)
		newleft.left = tl
		newleft.right = trl

		self.value = vr
		self.right = trr
		self.left = newleft
		return


	def rightrotate(self):
		v = self.value
		vl = self.left.value
		tll = self.left.left
		tlr = self.left.right
		tr = self.right
		
		newright = AVLTree(v)
		newright.right = tr
		newright.left = tlr
		
		self.right = newright
		self.value = vl
		self.left = tll
		return

	def insert(self,v):
		if self.isempty():
			self.value = v
			self.left = AVLTree()
			self.right = AVLTree()
			self.height = 1
			return
		
		if self.value == v:
			return

		if v < self.value:
			self.right.insert(v)
			self.rebalance()
			self.height = 1 + max(self.left.height, self.right.height)

		if v > self.value:
			self.right.insert(v)
			self.rebalance()
			self.height = 1 + max(self.left.height, self.right.right)
		
	def rebalance(self):
		if self.left == None:
			hl = 0
		else:
			hl = self.left.height
			
		if self.right == None:
			hr = 0
		else:
			hr = self.right.height
		
		if hl - hr > 1:
			if self.left.left.height > self.left.right.height:
				self.rightrotate()
			if self.left.left.height < self.left.right.height:
				self.left.leftrotate()
				self.rightrotate()
				self.updateheight()
			
		if hl - hr < -1:
			if self.right.left.height < self.right.right.height:
				self.leftrotate()
			if self.right.left.height > self.right.right.height:
				self.right.rightrotate()
				self.leftrotate()
			self.updateheight()
		
	def updateheight(self):
		if self.isempty():
			return
		else:
			self.left.updateheight()
			self.right.updateheight()
			self.height = 1 + max(self.left.height, self.right.height)
	
	def inorder(self):
		if self.isempty():
			return([])
		else:
			return(self.left.inorder() + [self.value] + self.right.inorder())
		
	def preorder(self):
		if self.isempty():
			return([])
		else:
			return([self.value] + self.left.preorder() + self.right.preorder())
		
	def postorder(self):
		if self.isempty():
			return([])
		else:
			return(self.left.postorder() + self.right.postorder() + [self.value])

A = AVLTree()
nodes = eval(input())
for i in nodes:
    A.insert(i)

print(A.inorder())
print(A.preorder())
print(A.postorder())
```

```Input
[1,2,3,4,5,6,7] #order of insertion
```

```Output
[1, 2, 3, 4, 5, 6, 7] #inorder traversal
[4, 2, 1, 3, 6, 5, 7] #preorder traversal
[1, 3, 2, 5, 7, 6, 4] #postorder traveral
```

# Greedy Algorithm

#### Interval Scheduling

- A greedy algorithm makes a sequence of locally optimal choices to achieve a globally optimum.
- Drastically reduces space to search for solution but we need to show proof that the local optimum choices lead to global optimum.

- **Interval Scheduling:** Choose the one which finishes the earliest.

###### Algorithm
1. Sort all jobs which are based on end time in increasing order.
2. Take the interval which has the earliest schedule
3. Repeat next steps until all jobs are processed:
	1. Eliminate all intervals which have start time less than selected interval's end time. (which will start before the current one ends).
	2. If interval has start time greater than current interval's end time, at it to set. Set current interval to new interval.
```Python
def intervalschedule(L):
	sortedL = sorted(L, key=2)
	accepted = [sortedL[0][0]]
	for i,s,f in sortedL[1:]:
		if s > L[accepted[-1]][2]:
			accepted.append(i)
	return accepted

#(job id,start time, finish time) in each tuple of list L
L = [(0, 1, 2),(1, 1, 3),(2, 1, 5),(3, 3, 4),(4, 4, 5),(5, 5, 8),(6, 7, 9),(7, 10, 13),(8, 11, 12)]
print(len(intervalschedule(L)))
```

```Output
4
```


#### Minimizing Lateness

- **Solution:** Select requests in increasing order of deadlines.

###### Algorithm
1. Sort all jobs in ascending order of deadlines.
2. Start with time `t=0`
3. For each job in the list:
	1. Schedule the job at time `t`
	2. Finishing time = `t` + `processing time of the job`
	3. `t` = Finish time
4. Return start time and finish time for each job

```Python
from opertor import itemgetter

def minimize_lateness(jobs):
	schedule = []
	max_lateness = 0
	t = 0

	sorted_jobs = sorted(jobs, key=itemgetter(2))

	for job in sorted_jobs:
		job_start_time = t
		job_finish_time = t + job[1]

		t = job_finish_time
		
		if(job_finish_time > job[2]):
			max_lateness = max(max_lateness, (job_finish_time - job[2]))
			schedule.append((job[0], job_start_time, job_finish_time))
	
	return max_lateness, schedule


jobs = [(1, 3, 6), (2, 2, 9), (3, 1, 8), (4, 4, 9), (5, 3, 14), (6, 2, 15)]
max_lateness, sc = minimize_lateness(jobs)
print ("Maximum lateness is :" + str(max_lateness))
for t in sc:
    print ('JobId= {0}, start time= {1}, finish time= {2}'.format(t[0],t[1],t[2]))
```

```Output
Maximum lateness is :1
JobId= 1, start time= 0, finish time= 3
JobId= 3, start time= 3, finish time= 4
JobId= 2, start time= 4, finish time= 6
JobId= 4, start time= 6, finish time= 10
JobId= 5, start time= 10, finish time= 13
JobId= 6, start time= 13, finish time= 15
```

#### Huffman Encoding

- In a tree for Huffman coding:
	- *Less frequent words are at the bottom leaves of the tree*. This is because we can afford to spend a bit more on characters which will be less frequent.
	- *And as we go up in the tree the more frequent the characters are* since they are more frequent so we want to spend less on them.
	- We read the code from the root of the tree till the left of the character. Every branch will either have a 0 or 1.
- Huffman coding trees are full, i.e. they don not have partial leaf nodes, it'll always be in pair. But not all leaf nodes are assigned a character.
- Given the above statement we also have to keep in mind that leaf nodes at the maximum depth will always have a pair which will not be empty.

###### Algorithm
1. Calculate the frequency of each character in the string.
2. Sort the characters in increasing order of frequency.
3. Make each unique character as a leaf node.
4. Create an empty node `z`, assign minimum frequency to the left child of `z` and the 5. Second minimum frequency to the right child of `z`.
6. Set the value of `z` as the sum of the below minimum frequencies.
7. Remove these two minimum frequencies from list of frequencies Q and add their 8. Sum to the list of frequencies.
9. Insert node `z` into the tree.
10. Repeat steps 3 to 7 for all the characters.
11. For each non-leaf node assign `0` to the left edge and `1` to the right edge.

> To check if a Huffman encoding is correct, check if one of the encoding of an alphabet can be consumed totally by prefix of another.

![[Huffman Encoding.png]]