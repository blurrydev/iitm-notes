# Lecture 1: Introduction to graphs

- A **graph** represents relationships between entities.
	- **Entities** are vertices or nodes.
	- **Relationships** are edges.
- A graph maybe *directed* or *undirected*.
	- A is a parent of B - *directed*
	- A is a friend of B - *undirected*
- **Paths** are sequences of connected edges.
- **Walks** are paths that crosses one vertex more than once.

#### Uses of graphs

- **Reachability:** Is there a path from *u* to *v*.
	- A graph is *connected* if all vertices are reachable from each other.
- **Graph coloring:** Color vertices with different color which are not connected by an edge.
- **Vertex cover:** Finding minimal number of vertices which will cover all edges.
- **Independent set**
- **Matching**

# Lecture 2: Representing Graphs

We can represent graphs using:

1. **Adjacency Matrix**
2.  **Adjacency list**

#### Adjacency Matrix
- n x n matrix
- Mat [i, j] = 1 if there is an edge

```Python
# for a directed graph

V = [0,1,2,3,4]
E = [(0,1), (0,2), (1,3), (1,4), (2,4), (2,3), (3,4)]
size = len(v) # size of the side of the square matrix

import numpy as np

AMat = np.zeros(shape=(size,size))

for (i,j) in E:
	AMat[i,j] = 1
print(AMat)
```

```Output

[[0. 1. 1. 0. 0.]
 [0. 0. 0. 1. 1.]
 [0. 0. 0. 1. 1.]
 [0. 0. 0. 0. 1.]
 [0. 0. 0. 0. 0.]]

# AMat[i,j] == 1 represent edge from i to j
```

```Python
# for undirected graph

V = [0,1,2,3,4]
E = [(0, 1), (0, 2), (1, 3), (1, 4), (2, 4), (2, 3), (3, 4)]
UE = E + [ (j,i) for (i,j) in E] # each edge represented by two tuple (u,v) and (v,u)
size = len(V)
import numpy as np
AMat = np.zeros(shape=(size,size))
for (i,j) in UE:
    AMat[i,j] = 1 # mark 1 if edge present in graph from i to j , otherwise 0
print(AMat)
```

```Output

[[0. 1. 1. 0. 0.]
 [1. 0. 0. 1. 1.]
 [1. 0. 0. 1. 1.]
 [0. 1. 1. 0. 1.]
 [0. 1. 1. 1. 0.]]

 # AMat[i,j] == 1 represent edge from i to j
```

#### Adjacency List
- Dictionary of list
- The dictionary will have keys containing vertex name
- And each dictionary will have values containing list of vertices which will have an edge from the key (vertex)

```Python
# for directed graph

V = [0,1,2,3,4]
E = [(0,1), (0,2), (1,3), (1,4), (2,4), (2,3), (3,4)]
size = len(v)

AList = {}
# In dictionay AList, for example, AList[i] = [j,k] represent two edge from i to j and i to k

for i in range(size):
	AList[i] = []

for (i,j) in E:
	AList[i].append(j)
print(AList)
```

```Output

{0: [1, 2], 1: [3, 4], 2: [4, 3], 3: [4], 4: []}

# for example, AList[i] = [j,k] represent two edge from i to j and i to k
```

```Python
# For undirected graph

V = [0,1,2,3,4]
E = [(0, 1), (0, 2), (1, 3), (1, 4), (2, 4), (2, 3), (3, 4)]
UE = E + [ (j,i) for (i,j) in E] # each edge represented by two tuple (u,v) and (v,u)

size = len(V)
AList = {} # In dictionay AList, for example, AList[i] = [j,k] represent two edge from i to j and i to k

for i in range(size):
    AList[i] = []
for (i,j) in UE:
    AList[i].append(j)
print(AList)
```

```Output

{0: [1, 2], 1: [3, 4, 0], 2: [4, 3, 0], 3: [4, 1, 2], 4: [1, 2, 3]}
# for example, AList[i] = [j,k] represent two edge from i to j and i to k
```

# Lecture 3: Breadth First Search

- BFS stands for Breadth-First Search and is used for traversing or searching a graph or a tree.
- Visits vertices level by level.
- Uses a queue to keep track of vertices to be visited.
- Marks each vertex as visited once it is processed.
- Can be used for finding the *shortest path, checking if a path exists, finding connected components*, etc.
- **Complexity** is $O(n^2)$ using *adjacency matrix* and $O(n+m)$ using *adjacency list* were $m << n^2$.
- Add parent information to *recover the path* to each reachable vertex.
- Maintain level information to *record length of shortest path* in terms of number of edges.

#### BFS Steps
1. Initialize a queue to store the vertices to be visited.
2. Push the starting vertex into the queue.
3. Mark the starting vertex as visited.
4. Repeat the following steps until the queue is empty: 
	a. Pop a vertex from the queue. 
	b. Visit the vertex. 
	c. For each unvisited adjacent vertex of the current vertex, push it into the queue, mark it as visited and continue with the next adjacent vertex.
5. Continue the loop until all vertices have been visited.

```Python
def neighbours(AMat, i):
	nbrs = []
	(rows, cols) = AMat.shape

	for j in range(cols):
		if AMat[i,j] == 1:
			nbrs.append(j)
	return(nbrs)
```

```Python
class Queue:
	def __init__(self):
		self.queue = []
	def addq(self, v):
		self.queue.append(v)
	def isempty(self):
		return (self.queue == [])
	def delq(self):
		v = None
		if not self.isempty():
			v = self.queue[0]
			self.queue = self.queue[1:]
		return(v)
	def __str__(self):
		return(str(self.queue))
```

##### BFS with Adjacency List

```Python

def BFSList(AList, v):
	visited = {}
	for i in AList.keys()
		visited[i] = False
	q = Queue()

	visited[v] = True
	q.addq(v)

	while(not q.isempty()):
		j = q.delq()
		for k in AList[j]:
			if (not visited[k]):
				visited[k] = True
				q.addq(k)
	return(visited)

AList ={0: [1, 2], 1: [3, 4], 2: [4, 3], 3: [4], 4: []}
print(BFSList(AList,0))
```

```Output
{0: True, 1: True, 2: True, 3: True, 4: True}
```

##### BFS with Adjacency Matrix

```Python
def neighbours(AMat,i):
    nbrs = []
    (rows,cols) = AMat.shape
    
    for j in range(cols):
        if AMat[i,j] == 1:
            nbrs.append(j)
        return(nbrs)

def BFS(AMat, v):
    (rows,cols) = AMat.shape
    visited = {}
    
    for i in range(rows):
        visited[i] = False
    q = Queue()
    visited[v] = True
    q.addq(v)
    
    while(not q.isempty()):
        j = q.delq()
        for k in neighbours(AMat,j):
            if (not visited[k]):
                visited[k] = True
                q.addq(k)
    return(visited)


V = [0,1,2,3,4]
E = [(0, 1), (0, 2), (1, 3), (1, 4), (2, 4), (2, 3), (3, 4)] 
size = len(V)

import numpy as np
AMat = np.zeros(shape=(size,size))
for (i,j) in E:
    AMat[i,j] = 1

print(BFS(AMat,0))
```

```Output
{0: True, 1: True, 2: True, 3: True, 4: True}
```

##### Find path of vertex v using BFS

> We just need to maintain a separate dictionary called parent which will help us backtrack the path using parent information. By default the value will be -1 so the starting vertex will have parent as -1.

```Python
def neighbours(AMat,i):
    nbrs = []
    (rows,cols) = AMat.shape
    
    for j in range(cols):
        if AMat[i,j] == 1:
            nbrs.append(j)
        return(nbrs)

def BFS(AMat, v):
	visited = {}
	parent = {}
    for i in range(rows):
        visited[i] = False
        parent[i] = -1
    q = Queue()
    visited[v] = True
    q.addq(v)
    
    while(not q.isempty()):
        j = q.delq()
        for k in neighbours(AMat,j):
            if (not visited[k]):
                visited[k] = True
                parent[k] = j
                q.addq(k)
    return(visited)


V = [0,1,2,3,4]
E = [(0, 1), (0, 2), (1, 3), (1, 4), (2, 4), (2, 3), (3, 4)] 
size = len(V)

import numpy as np
AMat = np.zeros(shape=(size,size))
for (i,j) in E:
    AMat[i,j] = 1

print(BFS(AMat,0))
```

##### Finding level of vertex v using BFS

> We will replace the visited dictionary with a dictionary called level which will maintain the level. It will be -1 by default which will also indicate that a vertex is unvisited if the value is -1

```Python
def neighbours(AMat,i):
    nbrs = []
    (rows,cols) = AMat.shape
    
    for j in range(cols):
        if AMat[i,j] == 1:
            nbrs.append(j)
        return(nbrs)

def BFS(AMat, v):
	level = {}
	parent = {}
    for i in range(rows):
        level[i] = -1
        parent[i] = -1
    q = Queue()
    level[v] = 0
    q.addq(v)
    
    while(not q.isempty()):
        j = q.delq()
        for k in neighbours(AMat,j):
            if (level[k] == -1):
                level[k] = level[j]+1
                parent[k] = j
                q.addq(k)
    return(visited)


V = [0,1,2,3,4]
E = [(0, 1), (0, 2), (1, 3), (1, 4), (2, 4), (2, 3), (3, 4)] 
size = len(V)

import numpy as np
AMat = np.zeros(shape=(size,size))
for (i,j) in E:
    AMat[i,j] = 1

print(BFS(AMat,0))
```


# Lecture 4: Depth First Search (DFS)

- Visits vertices by exploring as far as possible along each branch before backtracking.
- Uses a stack to keep track of vertices to be visited.
- Marks each vertex as visited once it is processed.
- Can be used for finding a path, finding all paths, topological sorting, etc.
- **Complexity** is $O(n^2)$ using *adjacency matrix* and $O(n+m)$ using *adjacency list* were $m << n^2$.
- Unlike BFS, the paths using DFS are not the shortest.

#### DFS Steps

1. Initialize a stack to store the vertices to be visited.
2. Push the starting vertex into the stack.
3. Mark the starting vertex as visited.
4. Repeat the following steps until the stack is empty: 
	a. Pop a vertex from the stack. 
	b. Visit the vertex. 
	c. For each unvisited adjacent vertex of the current vertex, push it into the stack, mark it as visited, and continue with the next adjacent vertex.
5. Continue the loop until all vertices have been visited.

```Python
class Stack:
	def __init__(self):
		self.stack = []
	def push(self, v):
		self.stack.append(v)
	def isempty(self):
		return(self.stack == [])
	def pop(self):
		v = None
		if not self.isempty():
			v = self.stack.pop()
		return(v)
	def __str__(self):
		return(str(self.stack))
```

##### DFS using Stack for adjacency list of graph

```Python
def DFSList(AList, v):
	visited = {}

	for i in AList.keys():
		visited[i] = False
		
	st = stack
	st.push(v)

	while(not st.isempty()):
		j = st.pop()
		if visited[j] == False:
			visited[j] = True
			for k in AList[j][::-1]:
				if (not visited[k]):
					st.push(k)
	return(visited)

AList ={0: [1, 2], 1: [3, 4], 2: [4, 3], 3: [4], 4: []}
print(DFSList(AList,0))
```

```Output
{0: True, 1: True, 2: True, 3: True, 4: True}
```

##### DFS Recursive (without external stack)

>- Here recursion will take care of the job of stack. 
>- We can either maintain the dictionaries 'visited' and 'parent' locally and implement inside the recursive call or maintain them globally and don't call them inside recursive function.
>- Here I will directly use the dictionaries globally

```Python
(visited, parent) = ({}, {})

def DFSInitList(AList):
	# Initialization

	for i in AList.keys():
		visited[i] = False
		parent[i] = -1
	return

def DFSList(AList, v):
	visited[v] = True

	for k in AList[v]:
		if (not visited[k]):
			parent[k] = v
			DFSList(AList, k)
	return

AList ={0: [1, 2], 1: [3, 4], 2: [4, 3], 3: [4], 4: []}
DFSInitListGlobal(AList)
DFSListGlobal(AList,0)
print(visited,parent)
```

```Output
{0: True, 1: True, 2: True, 3: True, 4: True} {0: -1, 1: 0, 2: 0, 3: 1, 4: 3}
```

##### DFS Global for adjacency matrix of graph

```Python
(visited, parent) = ({}, {})

def DFSInit(AMat):
	# Initialization
	(rows, cols) = AMat.shape

	for i in range(rows):
		visited[i] = False
		parent[i] = -1
	return

def DFSGlobal(AMat, v):
	visited[v] = True

	for k in neighbours(AMat, v):
		if (not visited[k]):
			parent[k] = v
			DFSGlobal(AMat, k)

	return

V = [0,1,2,3,4]
E = [(0, 1), (0, 2), (1, 3), (1, 4), (2, 4), (2, 3), (3, 4)] 
size = len(V)
import numpy as np
AMat = np.zeros(shape=(size,size))
for (i,j) in E:
    AMat[i,j] = 1
DFSInitGlobal(AMat)
DFSGlobal(AMat,0)
print(visited,parent)
```

```Output
{0: True, 1: True, 2: True, 3: True, 4: True} {0: -1, 1: 0, 2: 0, 3: 1, 4: 3}
```

# Lecture 5: Application of BFS & DFS

- BFS & DFS can be used to identify connected components in an undirected graph.
	- BFS and DFS  identify an *underlying tree*.
	- *Non-tree* edges generate cycles.
- In directed graph, non-tree edges can be:
	- **Forward**
	- **Backward**
	- **Cross**
- Directed graphs decompose into strongly connected components.
	- **Strongly connected components:** Where every vertex is reachable from every other vertex.
	- DFS numbering can be used to compute SCC decomposition

#### Identifying connected components

###### Algorithm
- Assign each vertex a component number, let's say -1
- *Start BFS/DFS from vertex 0*
- Initialize component number to 0
- All the visited nodes will form a connected component
- Assign each visited node component number 0
- *Pick smallest unvisited node j*
- Increment component number to 1
- Run BFS/DFS from node j
- Assign each visited node component number 1
- *Repeat until all nodes are visited*

```Python
def Components(AList):
	component = {}
	for i in AList.keys():
		component[i] = -1

	(compid, seen) = (0,0)

	while seen <= max(AList.keys()):
		startv = min([i for i in AList.keys() if component[i] == -1])
		visited = BFSList(AList, startv)
		for i in visited.keys():
			if visited[i]:
				seen = seen + 1
				component[i] = compid
			compid = compid + 1
		return(component)

AList = {0: [1], 1: [2], 2: [0], 3: [4, 6], 4: [3, 7], 5: [3, 7], 6: [5], 7: [4, 8], 8: [5, 9], 9: [8]}
print(Components(AList))
```

```Output
{0: 0, 1: 0, 2: 0, 3: 1, 4: 1, 5: 1, 6: 1, 7: 1, 8: 1, 9: 1}
```

#### BFS Tree
- Edges explored by BFS forms a tree.
- Any *non tree edge* creates a cycle.

#### DFS Tree
- Maintain a DFS counter, initially 0
- Increment counter each time we enter or exit a node.
- Each vertex is assigned an *entry number (pre)* & *exit number (post)*.

##### Undirected graphs
- Non tree edges generate cycles.

##### Directed graphs
- Only backward edges generate cycles.

- Let's say parent node is *u* and the child node is *v*.
- **Forward edges:** When the interval of `pre(u)` and `post(u)` *contains* the interval of `pre(v)` and `post(v)`.
- **Backward edges:** When the interval of `pre(v)` and `psot(v)` *contains* the interval of `pre(u)` and `post(u)`.
- **Cross edge:** When the interval of `pre(u)` and `post(u)` is *disjoint* from the interval of `pre(v)` and `post(v)`.

##### Code

```Python
(visited, pre, post) = ({}, {}, {})

def DFSInitPrePost(AList):
	# Initialization

	for i in AList.keys():
		visited[i] = False
		(pre[i], post[i]) = (-1, -1)
	return

def DFSListPrePost(AList, v, count):
	visited[v] = True
	pre[v] = count
	count = count+1

	for k in AList[v]:
		if (not Visited[k]):
			count = DFSListPrePost(AList, k, count)

	post[v] = count
	count = count + 1
	return(count)

AList = {0: [1, 4],1: [0],2: [],3: [],4: [0, 8, 9],5: [],6: [],7: [],8: [4, 9],9: [8, 4]}
DFSInitPrePost(AList)
print(DFSListPrePost(AList,0,0))
print(visited)
print(pre)
print(post)
```

```Output
10
{0: True, 1: True, 2: False, 3: False, 4: True, 5: False, 6: False, 7: False, 8: True, 9: True}
{0: 0, 1: 1, 2: -1, 3: -1, 4: 3, 5: -1, 6: -1, 7: -1, 8: 4, 9: 5}
{0: 9, 1: 2, 2: -1, 3: -1, 4: 8, 5: -1, 6: -1, 7: -1, 8: 7, 9: 6}
```
 
 ###### Code summary
 - This function DFSListPrePost() takes in an adjacency list of a graph, a starting node, and a counter that keeps track of pre-order and post-order numbers.
- The function starts by marking the current node as visited and assigning the current pre-order number to the node.
- It then recursively calls itself on each unvisited neighbor of the current node.
- After visiting all neighbors, the function assigns the current post-order number to the current node and returns the updated counter.
- The function updates the count for each recursive call, so that each node gets a unique pre-order and post-order number.
- The function uses the visited, pre, and post dictionaries to keep track of which nodes have been visited and what their pre-order and post-order numbers are.

# Lecture 6: Intro to Directed Acyclic Graphs

- DAGs are a natural way to represent dependencies.
- These arise in many contexts:
	- Pre-requisites between courses for completing a degree.
	- Recipe for cooking
	- Construction projects.
- Problems to be solved in DAGs
	- Topological sorting
	- Longest paths

# Lecture 7: Topological Sort

1. Topological Sorting is a linear ordering of the nodes in a directed acyclic graph (DAG) such that for every directed edge `(u, v)`, node `u` comes before node `v` in the ordering.
    
2. The Topological Sorting algorithm can be used to find the order in which a set of tasks can be executed, given their dependencies.
    
3. The Topological Sorting algorithm works only for directed acyclic graphs (DAGs), i.e., graphs that do not have cycles.
    
4. The algorithm starts by finding the nodes that have no incoming edges (i.e., nodes with indegree 0) and adding them to a list.
    
5. It then removes those nodes and their outgoing edges from the graph and repeats the process with the remaining nodes, until all nodes have been processed.
    
6. The final list of nodes in the order they were processed is the topological sort of the graph.
    
7. The Topological Sorting algorithm can be implemented using both the adjacency matrix and adjacency list representations of the graph.
    
8. The time complexity of the Topological Sorting algorithm is O(V+E), where V is the number of nodes and E is the number of edges in the graph.
    
9. The Topological Sorting algorithm can be used to detect cycles in a graph. If the algorithm cannot find any nodes with indegree 0, it means the graph has a cycle.

#### How to calculate indegree?

1. Adjacency matrix: In an adjacency matrix, each row and column represents a node, and the matrix entry (i, j) is 1 if there is an edge from node i to node j, and 0 otherwise. 
	- To compute the indegree of each node, iterate over each column of the matrix and count the number of non-zero entries in that column. This count is the indegree of the corresponding node. In other words, the indegree of node j is the sum of matrix entries in the j-th column.
    
2. Adjacency list: In an adjacency list, each node has a list of its outgoing neighbors. 
	- To compute the indegree of each node, iterate over each node and its neighbors, and increment the indegree of each neighbor by 1. This can be done using a dictionary to keep track of the indegrees. For example, you can initialize a dictionary with keys corresponding to each node, and values initialized to 0. Then, for each node and its neighbors, increment the indegree of each neighbor in the dictionary. Once you have iterated over all nodes and their neighbors, the dictionary will contain the indegree of each node.

#### Topological sort using Adjacency matrix

```Python
def toposort(AMat):
	(rows, cols) = AMat.shape
	indegree = {}
	toposortlist = []

	# Calculating indegree
	for c in range(cols):
		indegree[c] = 0
		for r in range(rows):
			if AMat[r,c] == 1:
				indegree[c] = indegree[c] + 1

	for i in range(rows):
		j = min([k for k in range(cols) if indegree[k] == 0])
		toposortlist.append(j)
		indegree[j] = indegree[j] - 1   # This is reduced to -1 so that this node can be removed from the existing calculation

		for k in range(cols):
			if AMat[j,k] == 1:
				indegree[k] = indegree[k] - 1
		
	return(toposortlist)

edges=[(0,2),(0,3),(0,4),(1,2),(1,7),(2,5),(3,5),(3,7),(4,7),(5,6),(6,7)]
size = 8
import numpy as np
AMat = np.zeros(shape=(size,size))
for (i,j) in edges:
    AMat[i,j] = 1
print(toposort(AMat))
```

```Output
[0, 1, 2, 3, 4, 5, 6, 7]
```

#### Topological sort for Adjacency list

```Python
def toposortlist(AList):
	(indegree, toposortlist) = ({},[]) 
	zerodegree = Queue()

	for u in AList.keys():
		indegree[u] = 0

	for u in AList.keys():
		for v in AList[u]:
			indegree[v] = indegree[v] + 1

	for u in AList.keys():
		if indegree[u] == 0:
			zerodegreeq.addq(u)

	while (not zerodegreeq.isempty()):
		j = zerodegreeq.delq()
		toposortlist.append(j)
		indegree[j] = indegree[j] - 1  # this is done to remove this node from calculation

		for k in AList[j]:
			indegree[k] = indegree[k] - 1
			if indegree[k] == 0;
				zerodegreeq.addq(k)
	return(toposortlist)


AList={0: [2, 3, 4], 1: [2, 7], 2: [5], 3: [5, 7], 4: [7], 5: [6], 6: [7], 7: []}
print(toposortlist(AList))
```

```Output
[0, 1, 3, 4, 2, 5, 6, 7]
```

