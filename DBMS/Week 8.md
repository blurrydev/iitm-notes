# Tree

- A tree with $n$ *nodes* will have $n-1$ *edges*.
- **Arity** is the number of children of a node
- **Arity of tree** is the *maximum arity* of the nodes of a tree.

# Binary Tree

- **Maximum number of nodes** at *level* $l$ of a binary tree is $2^l$
- **Total number of nodes** in a binary tree *upto level* $l$ is $2^{l+1}-1$
- Level always starts from 0

# Binary Search Tree

- The value of each node in the *left sub-tree* should be **lesser** than the value of it's root.
- The value of each node in the *right sub-tree* should be **greater** than the value of it's root.

# Magnetic Disk

- Every face of the platter have tracks
- And every track is divided into equal sectors.
- **Sector** is the smallest unit in a magnetic disk
- **Seek time** is the time required to position the R/W head into the desired position
- **Rotational Latency** is the time required to rotate into desired sector

- **Average rotational latency**: $1/2 \times$ time required to complete one rotation

- **Access time:** Seek time + Rotational Latency 
>In numerical if rotational latency is not given then we will take average rotational latency
>Access time is for per sector

- **Disk Capacity:** Total sectors present $\times$ Number of bytes present in one sector

- **Transfer Rate =**  Capacity of one track / Time required for 1 rotation

# Buffer Replacement Policy

- **Least Recently Used**