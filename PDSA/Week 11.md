# Network Flow

### Rules

1. There should not be any accumulation of entity in any point of the network.
2. Maximize the flow.
3. Follow capacity constraints.

It will be a directed graph and there will be a weight on the graph, that weight will be it's capacity and we cannot send more than that capacity through that edge.

### Possible Questions from this concept

1. Given a graph what will be the maximum possible flow?

	#### Ford Fulkerson Algorithm
	1. Initialize the graph with random but correct flow.
	2. Draw the residual graph.
	3. Find the augmenting path in the residual graph.
	4. Find the bottleneck capacity of the augmented path from the last step.
	5. For every edge in G (*the original graph*) on the augmented path 
		- Add bottle neck capacity to the current flow if the direction of G and RG (*Residual Graph*) is same.
		- Else if they are in opposite direction then substract the bottle neck capacity.

- **Complexity:** Directly proportional to the highest capacity of the graph.


2. Given a graph what can be the minimum cut?

- **Cut:** A cut is a partition of vertices in a flow graph such that it disconnects the source and the sink.
- Flow through *any cut is same* and is equal to the *flow of the network*.
- The above condition holds true at any flow state of the network.

### Capacity of the cut

Let's say there is a cut which divides the graph into two sets $S_1$ and $S_2$.

- Now let's say the source is in $S_1$ and the sink is in $S_2$.
- So the capacity of the cut is the sum of the capacity of the edges that the coming from $S_1$ to $S_2$.
- Keep in mind that we're dealing with capacity and not flow.


- *Flow* through the cut is equal to or smaller than the capacity if the cut.
- *The maximum flow is always equal to the minimum capacity of the cut.*

# Complexity Classes

Follow [Week 11 Complexity classes](Week%2011%20Complexity%20classes.canvas)

- For both `N-class` and `NP-class` takes polynomial time to verify.
- `N-class` takes polynomial time to solve.
- `NP-class` takes exponential time to solve.

These concepts are used for two cases:

1. To prove that a problem is intractable.
2. To solve a problem for which we don't know the algorithm.

We achieve this by using *reduction*.

- **Reduction:** Converting a problem into another problem.

- We convert the inputs of problem $A$ into a format such that they represent the inputs of problem $B$.
- Now use problem $B$ to get the answers, finally reverse map the outputs of B into a format which resembles the output of problem $A$.

>If B has a known polynomial time algorithm and if we can reduce A to B then, A can also be solved using B in polynomial time. 


- When I reduce a problem $A$ into another problem $B$ then $B$ will always be harder to solve than $A$.

#### Now to prove that a problem is intractable

1. We will take a problem which we already know to be intractable.
2. Then we take our problem and reduce it to the problem from step 1 which is intractable.
3. If we can successfully do it then we can say that our problem is atleast as hard (if not more) as the intractable problem from step 1 and hence proved.
