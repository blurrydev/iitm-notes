# Shortest Path in Weighted Graphs

^b7cf0d

- In a weighted graph, each edge has a cost.
- We represent the weights along with the vertices to keep a track of the weight.
- In a weighted graph we will consider the weights instead of  number of edges. As we go from one vertex to another we will keep adding the weights.
- Different shortest path problems
	- *Single Source* shortest path.
	- *All pairs* shortest path.
- Negative edge weights
	- Should **not** have negative cycles.
	- Without negative cycles, shortest path can still be defined.

```Python
dedges = [(0,1,10), (0,2,80), (1,2,6), (1,4,20), (2,3,70), (4,5,50), (4,6,5), (5,6,10)]
size = 7

import numpy as np

W = np.zeros(shape=(size,size,2))

for (i,j,w) in dedges:
	W[i,j,0] = 1
	W[i,j,1] = w

print(W)
```

```Python
dedges = [(0,1,10), (0,2,80), (1,2,6),(1,4,20), (2,3,70), (4,5,50), (4,6,5), (5,6,10)]
size = 7

WL = {}

for i in range(size):
	WL[i] = []
for (i,j,d) in dedges:
	WL[i].append((j,d))

print(WL)
```

# Dijkstra's Algorithm

^e7a323

- It computes the *single source shortest path*.
- Uses *greedy* strategy.
- Cannot work in graphs with negative edges.
- Complexity is $O(n^2)$, even with adjacency lists.
- Dijkstra's algorithm can handle disconnected graphs but will only find the shortest path for the connected component containing the source vertex.

#### Algorithm
1.  Initialize the distance of the starting node as 0, and the distance of all other nodes as infinity. Set all nodes as unvisited.
2.  Select the node with the smallest distance and mark it as visited.
3.  For each neighbor of the selected node, calculate the distance from the starting node to that neighbor through the selected node.
4.  If the calculated distance is less than the previously recorded distance, update the distance.
5.  Repeat steps 2-4 until all nodes have been visited.
6.  Once all nodes have been visited, the shortest path from the starting node to any other node can be determined by following the path of smallest recorded distances.

#### Dijkstra's Algorithm with Adjacency Matrix

```Python
def dijkstra(WMat,s):
	(rows, cols, x) = WMat.shape
	infinity = np.inf

	(visited, distance) = ({}, {})

	for v in range(rows):
		(visited[v], distance[v]) = (False, infinity)

	distance[s] = 0
	for u in range(rows):
		nextd = min([distance[v] for v in range(rows) if not visited[v]])
		nextvlist = [v for v in range(rows) if (not visited[v]) and (distance[v] == nextd)]

		if nextvlist == []:
			break

		nextv = min(nextvlist)
		visited[nextv] = True
		for v in range(cols):
			if WMat[nextv, v, 0] == 1 and (not visited[v]):
				distance[v] = min(distance[v], distance[nextv]+WMat[nextv, v, 1])

	return(distance)


dedges = [(0,1,10),(0,2,80),(1,2,6),(1,4,20),(2,3,70),(4,5,50),(4,6,5),(5,6,10)]
size = 7
import numpy as np
W = np.zeros(shape=(size,size,2))
for (i,j,w) in dedges:
    W[i,j,0] = 1
    W[i,j,1] = w
print(dijkstra(W,0))
```

```Output
{0: 0, 1: 10.0, 2: 16.0, 3: 86.0, 4: 30.0, 5: 80.0, 6: 35.0}
```

#### Dijkstra's Algorithm with Adjacency list

```Python
def dijkstralist(WList, s):
	infinity = np.inf

	for v in WList.keys():
		(visited[v], distance[v]) = (False, infinity)

	distance[s] = 0

	for u in WList.keys():
		nextd = min([distance[v] for v in WList.keys() if not visited[v]])
		nextvlist = [v for v in WList.keys() if (not visited[v]) and (distance[v] == nextd)]

		if nextvlist == []:
			break

		nextv = min(nextvlist)
		visited[nextv] = True

		for (v,d) iin Wlist[nextv]:
			if not visited[v]:
				distance[v] = min(distance[v], distance[nextv] + d)

	return(distance)


dedges = [(0,1,10),(0,2,80),(1,2,6),(1,4,20),(2,3,70),(4,5,50),(4,6,5),(5,6,10)]
size = 7
for i in range(size):
    WL[i] = []
for (i,j,d) in dedges:
    WL[i].append((j,d))
print(dijkstralist(WL,0))
```

```Output
{0: 0, 1: 10, 2: 16, 3: 86, 4: 30, 5: 80, 6: 35}
```

# Bellman Ford Algorithm

This algorithm uses brute force to update distances for every vertex.

- It is a *dynamic programming based algorithm*.
- It can handle graphs with *negative edges* but *not negative cycles*.
- It can *detect negative cycles* in the graph. In case there is a negative cycle then the graph will be unstable and will not return a shortest path.
- It can handle disconnected graphs.
- It works for *both directed and non directed graphs*.

#### Algorithm
1. Initialize the distance array: Set the distance of the source vertex to 0 and the distances of all other vertices to infinity.
2. Relax all edges: 
	1. Repeat the same for (v-1) times, where `v` is the number of edges in the graph.
	2. For each edge (u,v) with weight w, if the distance to `u` plus `w` is less than the distance to `v`, update the distance of `v` to distance of `v` + `w`.
3. Check for negative edges:
	After relaxing all edges `v-1` times, check for negative edge cycles.
	For each edge (u,v) with weight w, if the distance to `u` plus `w` is less than the distance to `v`, there exists a negative weight cycle.
4. Print distance array.

#### Bellman Ford with Adjacency matrix

Complexity = $O(n^3)$

```Python
def bellmanford(WMat, s):
	(rows, cols, x) = WMat.shape
	infinity = np.inf
	distance = {}

	for v in range(rows):
		distance[v] = infinity

	distance[s] = 0

	for i in range(rows):
		for u in range(rows):
			for v in range(cols):
				if Wmat[u,v,0] == 1:
					distance[v] = min(distance[v], distance[u] + WMat[u,v,1])

	return(distance)


edges = [(0,1,10),(0,7,8),(1,5,2),(2,1,1),(2,3,1),(3,4,3),(4,5,-1),(5,2,-2),(6,1,-4),(6,5,-1),(7,6,1)]
size = 8
import numpy as np
W = np.zeros(shape=(size,size,2))
for (i,j,w) in edges:
    W[i,j,0] = 1
    W[i,j,1] = w    
print(bellmanford(W,0))
```

```Output
{0: 0, 1: 5.0, 2: 5.0, 3: 6.0, 4: 9.0, 5: 7.0, 6: 9.0, 7: 8.0}
```

#### Bellman Ford Algorithm with adjacency list

Complexity = $O(V * E)$ `V` is number of vertices and `E` is the number of edges.

```Python
def bellmanfordlist(WList, s):
	infinity = np.inf
	distance = {}

	for v in WList.keys():
		distance[v] = infinity

	distance[s] = 0

	for i in WList.keys():
		for u in WList.keys():
			for (v,d) in WList[u]:
				distance[v] = min(distance[v], distance[u] + d)

	return(distance)


edges = [(0,1,10),(0,7,8),(1,5,2),(2,1,1),(2,3,1),(3,4,3),(4,5,-1),(5,2,-2),(6,1,-4),(6,5,-1),(7,6,1)]
size = 8
WL = {}
for i in range(size):
    WL[i] = []
for (i,j,d) in edges:
    WL[i].append((j,d))
print(bellmanfordlist(WL,0))
```

```Output
{0: 0, 1: 5, 2: 5, 3: 6, 4: 9, 5: 7, 6: 9, 7: 8}
```

# Floyd Warshall Algorithm

- Warshall's algorithm is an alternative way to calculate *transitive closure*.
- Adapt Warshall's algorithm to compute all pairs shortest paths
	- $SP^k$[i, j] is the length of the shortest path from i to j using vertices {0,1,..., k-1}
	- $SP^n$[i,j] is the length of the overall shortest path.
	- Floyd-Warshall algorithm
- Works with negative edge weights but *not negative cycles*
- Simple nested loop implementation, time $O(n^3)$.
- Space can be limited to $O(n^2)$ bu reusing two "slices" $SP$ & $SP$"
- No guarantee of uniqueness, there are several shortest path between two nodes.
- Does not work with negative edges in an undirected graph as it will be declared as a negative weight cycle.

> Can detect negative edge cycle when any diagonal distance goes negative



#### Algorithm
1.  Initialization: Create a 2-dimensional array `SP` of size `n x n`, where `n` is the number of vertices in the graph. For each pair of vertices `(i,j)`, initialize `SP[i][j]` to the weight of the edge from vertex `i` to vertex `j`. If there is no edge between vertices `i` and `j`, then set `SP[i][j]` to infinity.
    
2.  For each vertex `k` from `1` to `n`, compute the shortest path between every pair of vertices `(i,j)` that passes through `k`. To do this, update `SP[i][j]` as follows:
    
    `SP[i][j] = min(SP[i][j], SP[i][k] + SP[k][j])`
    
    This means that the shortest path from vertex `i` to vertex `j` that passes through `k` is the minimum of the current shortest path from `i` to `j` and the sum of the shortest path from `i` to `k` and the shortest path from `k` to `j`.
    
3.  After the step 2 is complete, the `SP` array will contain the shortest path between every pair of vertices in the graph.

```Python
def floydwarshall(WMat):
	(rows, cols, x) = Wmat.shape
	infinity = np.inf

	SP = np.zeros(shape=(rows, cols, cols+1))

	for i in range(rows):
		for j in range(cols):
			if WMat[i,j,0] == 1:
				SP[i,j,0] = WMat[i,j,1]

	for k in range(1, cols+1):
		for i in range(rows):
			for j in range(cols):
				SP[i,j,k] = min(SP[i, j, k], SP[i,k-1,k-1]+SP[k-1,j,k-1])

	return(SP[:,:, cols])


edges = [(0,1,10),(0,7,8),(1,5,2),(2,1,1),(2,3,1),(3,4,3),(4,5,-1),(5,2,-2),(6,1,-4),(6,5,-1),(7,6,1)]
size = 8
import numpy as np
W = np.zeros(shape=(size,size,2))
for (i,j,w) in edges:
    W[i,j,0] = 1
    W[i,j,1] = w    
print(floydwarshall(W))
```

```Output
[[641.   5.   5.   6.   9.   7.   9.   8.]
 [641.   1.   0.   1.   4.   2. 641. 641.]
 [641.   1.   1.   1.   4.   3. 641. 641.]
 [641.   1.   0.   1.   3.   2. 641. 641.]
 [638.  -2.  -3.  -2.   1.  -1. 638. 638.]
 [639.  -1.  -2.  -1.   2.   1. 639. 639.]
 [637.  -4.  -4.  -3.   0.  -2. 637. 637.]
 [638.  -3.  -3.  -2.   1.  -1.   1. 638.]]
```

# Minimum Cost Spanning Trees

## Tree Facts
1. A tree on `n` vertices has exactly `n-1` edges.
2. Adding an edge to a tree must create a cycle.
3. In a tree every pair of vertices is connected by a unique path.

Any two of the following facts about a graph `G` will imply that it's a tree:
	1. `G` is connected
	2. `G` is acyclic
	3. `G` has `n-1` edges

There are two strategies to build a minimum cost spanning tree:
	1. *Prim's algorithm:* Start with the smallest edge and grow a tree.
	2. *Kruskal's algorithm:* Scan edges in ascending order of weight to connect components without forming cycles.

## Prim's Algorithm

1. Start from any vertex
2. Check the vertices connected to this vertex and choose the one with with the minimum cost.
3. Now keep the cost of the other unchosen vertex in mind and find next vertex with the lowest cost.
4. Connect the vertices as you move towards the lower cost vertices but keep in mind that there should not be a loop
5. https://www.youtube.com/watch?v=_KX8GDvRzBc

#### Code

```Python
def primlist(WList):
	infinity = np.inf
	(visited, distance, TreeEdges) = ({}, {}, [])

	for v i n WList.keys():
		(visited[v], distance[v]) = (False, infinity)

	visited[0] = True
	for (v,d) in WList[0]:
		distance[v] = d

	for i in WList.keys():
		minDist = infinity
		nextv = None

		for u in WList.keys():
			for (v,d) in WList[u]:
				if visited[u] and (not visited[v]) and d < minDist:
					minDist = d
					nextv = v
					nexte = (u,v)

		if nextv is None:
			break

		visited[nextv] = True
		TreeEdges.append(nexte)

		for (v,d) in WList[nextv]:
			if not visited[v]:
				distance[v] = min(distance[v], d)


	return (TreeEdges)

dedges = [(0,1,10),(0,3,18),(1,2,20),(1,3,6),(2,4,8),(3,4,70)]
edges = dedges + [(j,i,w) for (i,j,w) in dedges]
size = 5
WL = {}
for i in range(size):
    WL[i] = []
for (i,j,d) in edges:
    WL[i].append((j,d))
print(primlist(WL))
```


```Output
[(0, 1), (1, 3), (1, 2), (2, 4)]
```

##### Code Summary
1.  Initialize the `visited`, `distance`, and `TreeEdges` dictionaries/lists.
2.  Set all nodes in the `visited` dictionary to `False`, and set all distances in the `distance` dictionary to infinity.
3.  Set the distance of node 0 to 0.
4.  Iterate over the keys (nodes) in the `WList` dictionary:
    -   Find the node with the smallest distance that has not been visited.
    -   Add this node to the `TreeEdges` list.
    -   Update the distances of neighboring nodes.
5.  Return the `TreeEdges` list, which contains the edges of the minimum spanning tree.

#### Summary
- Implementation similar to Dijkstra's Algorithm
	- Update rule for distance is different
- Complexity is $O(n^2)$
- 

## Kruskal's Algorithm

#### Algorithm

1. Start with `n` components, each an isolated index.
2. Scan edges in ascending order of cost.
3. Whenever an edge merges disjoint components, add it to the MCST

#### Summary
- **Complexity:** $O(n^2)$
- If edge weights repeat then MCST will **not** be unique.

```Python
def kruskal(WList):
	(edges,component,TE) = ([],{},[])

	for u in WList.keys():
		# weight as first component to sort easily
		edges.extend([(d,u,v) for (v,d) in WList[u]])
		component[u] = u
	edges.sort()
    #print(edges)
    
    for (d,u,v) in edges:
        if component[u] != component[v]:
            TE.append((u,v))
            c = component[u]
            for w in WList.keys():
                if component[w] == c:
                    component[w] = component[v]
    return(TE)


dedges = [(0,1,10),(0,2,18),(1,2,6),(1,4,20),(2,3,70),(4,5,10),(4,6,10),(5,6,5)]
edges = dedges + [(j,i,w) for (i,j,w) in dedges]
size = 7
WL = {}
for i in range(size):
    WL[i] = []
for (i,j,d) in edges:
    WL[i].append((j,d))
print(kruskal(WL))
```

```Output
[(5, 6), (1, 2), (0, 1), (4, 5), (1, 4), (2, 3)]
```