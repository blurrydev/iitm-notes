# Indexing

- Indexing is used to speed up access to desired data.

- **Dense** is when there are `n` entries in the index table for `n` entries in the original table.
	- Number of entries in index is equal to the number of entries in the original table.
- **Sparse** is when we make one entry in the index table for each block in the original table.
	- Number of entries in index table is equal to number of blocks in the hard drive.
	- Can only be done when *data is ordered or sorted*.
	- The record which is used as `search key` is called *Anchor record*.
	- How to find record with search-key value `k`?
		- Find the index record with largest key value which is smaller than `k`.
		- Search file sequentially with the record to which the above index record points.
- Each index table has a `key` and a `pointer`.
- Index is always sorted so the time required to search is $log_2$ $n$.

## Types of indices

- **Ordered file:** All data are ordered or sorted.
- **Unordered file:** Data not ordered or sorted.
- **Key:** If data has all unique elements which can be made key.
- **Non Key:** If data has no unique element which can be made key.

![[primary_secondary_clustered.png]]

There are **three** types of indices:
1. Primary: 
	- The index whose key specifies the sequential order of the file. Like primary key in database schema.
	- Sparse
	- Also called *clustering index*
	- The search key of the primary index may or may not be a primary key.
2. Clustered: Here we cluster data and one key points to the first value of the 
3. Secondary:
	 - A key which specifies an order different from the sequential order of the file.
	 - Also called *non-clustering index*.

 - **Index Sequential file:** Ordered sequential file with primary index.

> - Secondary index can only be made from unordered file
> - Ordered files can create primary or clustered index depending upon if the values are unique or not.

## Sparse VS Dense Index comparison

The key differences between dense and sparse indexes are as follows:

1. **Size:** Dense indexes are larger than sparse indexes because they contain an entry for each record in the table, while sparse indexes only contain entries for a subset of the records.
2. **Speed:** Dense indexes can be faster to search because they provide direct access to the data, while sparse indexes require additional disk I/O to retrieve the data. (*in terms of locating data*)
3. **Insertion and deletion:** Dense indexes are slower for insertion and deletion operations because all the entries must be shifted or reorganized when a record is added or removed. Sparse indexes are faster for insertion and deletion because only the affected entries need to be updated.
4. **Flexibility:** Sparse indexes are more flexible than dense indexes because they can be easily added or removed from the index without affecting the underlying data. Dense indexes are more rigid and require more maintenance to keep them up-to-date.
5. **Space utilization:** Sparse indexes are more space-efficient than dense indexes because they only store entries for a subset of the records. Dense indexes use more disk space because they contain an entry for each record in the table.

# Secondary Indices

- Secondary indices are done on unordered data as mentioned in the diagram above.
- And since secondary indices work even non key values so there might be one secondary index pointing to multiple locations.
	- Hence we will keep a middle layer where the secondary index points and the middle layer has addresses and pointers to all other locations with the same name.

# Multi-level index

- This is done when *the size of the index is more than that of the available memory*.
- The top level indices points to the next level indices.
	- Which in turn points to the lower level indices or the data itself.
- Indices at each level *must be updated* on insertions or deletions.

# Insertions and Deletions

## Insertion
Insertion is the process of adding new data or records to an existing database. When new data is added, the database needs to be updated so that it can store and retrieve the new data. There are different ways to perform an insertion in a database. One common method is to use the SQL INSERT statement, which adds a new row to a table.

The basic steps involved in an insertion operation are:
1. The system identifies the appropriate location for the new record based on the indexing scheme used.
2. The new record is then inserted at the appropriate location, and the index is updated to reflect the new record.

## Deletion
Deletion is the process of removing data or records from an existing database. When data is deleted, the database needs to be updated so that it can reflect the changes. There are different ways to perform a deletion in a database. One common method is to use the SQL DELETE statement, which removes one or more rows from a table.

The basic steps involved in a deletion operation are:
1. The system identifies the record or records that need to be deleted based on the indexing scheme used.
2. The record or records are then deleted from the table, and the index is updated to reflect the changes.

It's important to note that *when a record is deleted, any indexes that point to that record must also be updated to reflect the deletion*. This can be a time-consuming operation for large databases, which is why it's important to choose an efficient indexing scheme and keep the database optimized for performance.


# 2-3-4 Tree

## Why use tree data structure?

As we learnt above that during insertion and deletion we need to update all index table, so it becomes a mess in multi-level indexing hence we will implement tree structure to overcome this issue.

## Properties

- All leaves are at the same depth, i.e, height of all leaf nodes are same.
- All data is kept in sorted order

- There are 3 kinds of nodes satisfying key relationships:
	- **2-node**: Contains a *single* data item (*S*) and *two* links.
	- **3-node**: Contains *two* data items (*S, L*) and *three* links.
	- **4-node**: Contains *three* data items (*S, M, L*) and *four* links.

![[2-3-4 trees.png]]

- **Max keys:** `p` - 1
- **Min Keys:** `p/2` - 1

![[tree_structure.png]]

- From the above diagram it is clear that number of `record pointer` is equal to the number of `key` which is always *one less than the order (p)*.
- **Deletion** in 2-3-4 trees happen only at the leaf node.
	- If the element that we want to delete is a *leaf node with atleast two elements* then we can **directly delete it**.
	- If the element that we want to delete is in internal node then we need to shift the element from internal node to leaf node, *by following inorder predecessor*, and then delete it.
	- **How to decide when to use inorder successor or predecessor?**
		- We will always try to adjust it accordingly based on which node has two or more children and try to avoid the leaf node with one child.
	- **What do we do when there is just one child for both nodes?**
		- In such case we will merge the node with the bottom two to make it into a node with three elements and then delete the element from the node.
		- **This is only applicable to intermediate nodes and not leaf nodes.**
		- There's no way we can delete a leaf node with single value, if it's parent node also has single element.
		- However, if the parent of a leaf node with single element has two or more elements then we can merge the leaf node with one of the element from the parent node and then delete it.
		- This is done to preserve the property that says that *all leaf nodes will be at the same level*.

> - *Inorder predecessor is the process where we find the element which is smaller than the current value but largest of the values less than the current value.*
> - Inorder successor is same as above but here instead of taking the highest smallest value we take the smallest highest values, i.e. smallest value which is higher than the current value.

### Summary of deletion:

When we delete a node from a 2-3-4 tree, there are three possible scenarios:
1. **Case 1: Deleting a node from a leaf node with more than one key**
   In this case, we simply remove the key and the corresponding record pointer from the leaf node. This does not violate any rules of the 2-3-4 tree.
2. **Case 2: Deleting a node from a leaf node with only one key**
   In this case, we remove the key and the corresponding record pointer from the leaf node. Since the leaf node must have at least one key, we need to redistribute keys from a neighboring leaf node or merge two leaf nodes to ensure that the tree remains balanced.
3. **Case 3: Deleting a node from an internal node**
   When we delete an internal node, we need to replace it with the minimum key from its right sub-tree. This ensures that the tree remains balanced and that the keys are in order. We then delete the minimum key from the right sub-tree.

# B-Tree

B-Tree stands for *Balanced Binary Tree*.

- **Order:** Maximum number of children parent can have. Let's say that the order of a B-tree is `p`, then

![[Order relation.png]]

- **Record Pointer:** A record pointer is a pointer to a specific record in a file or database. When a key is searched for in a B-tree, the record pointer associated with that key is used to retrieve the corresponding record. This allows for efficient retrieval of individual records.

- **Block Pointer:** A block pointer is a pointer to another node in the B-tree. Since B-trees are typically stored on disk or other secondary storage devices, it is important to minimize the number of disk accesses required to search the tree. By using block pointers, B-trees can be efficiently navigated with a minimal number of disk accesses.

- **Key:** Key tell us on what base we're searching for the pointer.
	- Number of `Keys` = Number of `record pointers`

> Number of keys is always 1 less than number of children.

#### How to solve finding order problems?

1. Keep this concept in mind. 
	
	Total number of `block pointers times size of each block pointer` plus number of `keys times size of each key `plus total `number of record pointers times size of each pointer` has to be *less than or equal to the size of the block pointer*.

2. Solve the inequality and find n (*the order*).

# Difference between B-Tree and B+ Tree

