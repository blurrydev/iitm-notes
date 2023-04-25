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

# B+ Tree

## Difference between B-Tree and B+ Tree

1. **Node Structure:** In a B-tree, each node contains both keys and pointers to child nodes or data. In a B+ tree, only the leaf nodes contain keys and data, while the internal nodes only contain keys and pointers to child nodes.
2. **Fanout:** B+ trees have a larger fanout than B-trees, meaning they can store more keys in each node. This results in fewer levels in the tree, which makes searching and traversing faster.
3. **Indexing:** B-trees are used for both primary and secondary indexing, while B+ trees are primarily used for secondary indexing.
4. **Sequential Access:** Because B+ trees store all data in the leaf nodes, they are optimized for sequential access. This makes them a good choice for applications that need to perform range queries or other operations that involve sequential data access.
5. **Range Queries:** B+ trees are better suited for range queries because all the data is stored in the leaf nodes. In a B-tree, range queries may require traversing multiple levels of the tree to find all the relevant data.
6. **Duplicate Keys:** B+ trees allow duplicate keys in the leaf nodes, while B-trees do not. This means that B+ trees can be used for applications that need to store multiple records with the same key value.

Overall, B+ trees are optimized for disk-based storage and are often used in databases and file systems. B-trees, on the other hand, are used in a wider range of applications, including in-memory data structures and databases.

> Only leaf node will contain the duplicate value and not the intermediate node.

# Advantages and Disadvantages

**Advantages of B-tree:**
- B-trees are well-suited for storing large amounts of data efficiently.
- They have a relatively balanced tree structure which allows for efficient search and retrieval operations.
- They have good locality of reference, which means that data accesses can be made more efficiently.
- B-trees can be used in a wide range of applications, including file systems, databases, and indexing.

**Disadvantages of B-tree:**
- B-trees have a more complex structure than some other data structures, which can make them harder to understand and implement.
- Inserting and deleting data from a B-tree can be more complex and slower than some other data structures.
- B-trees are not as space-efficient as some other data structures, since they require additional storage for the tree structure.

**Advantages of B+ tree:**
- B+ trees are well-suited for applications that require efficient range queries.
- They have a more optimized structure than B-trees, with all data stored in the leaf nodes and internal nodes only containing keys and pointers.
- B+ trees have good locality of reference, which means that data accesses can be made more efficiently.
- They have a relatively balanced tree structure which allows for efficient search and retrieval operations.

**Disadvantages of B+ tree:**
- B+ trees can be more complex to implement than some other data structures, due to their more optimized structure.
- B+ trees are not as space-efficient as some other data structures, since they require additional storage for the tree structure.
- Inserting and deleting data from a B+ tree can be more complex and slower than some other data structures, due to the need to rebalance the tree.

# Hashing

- Similar to the one taught in PDSA
- We can use either open hashing or closed hashing
- Used on *search keys*.

# Bit map indexing

- Bitmap Index is a type of index used in databases to quickly retrieve data based on Boolean conditions.
- It represents the existence or non-existence of a value in a column using bitmaps, which are arrays of bits (0 or 1).
- Each bit in the bitmap corresponds to a unique value in the indexed column, and its value is set to 1 if the value exists in a row or 0 if it does not.
- Bitmap Index is best suited for columns with low cardinality, i.e., a small number of distinct values. 
- It is most efficient for read-heavy workloads and can speed up query performance significantly.
- Bitmap Index can be used for both equality and range queries.
- It requires additional storage space for the bitmap indexes, which can be a disadvantage for large datasets.
- It can also be slower for write-heavy workloads as updating a row requires updating the corresponding bitmaps.
- Bitmap Index is most commonly used in data warehousing applications, where fast retrieval of large datasets is a requirement.

# Dynamic Hashing

## Extendable Hashing

- Set the initial global depth of the directory to 1 and create a directory with two entries.
- Each entry in the directory points to a bucket of fixed size. Initially, create two buckets and assign each entry in the directory to one of the buckets.
- When a new record needs to be inserted, compute its hash value and take the least significant (global depth) bits of the hash value to determine the bucket that it should be inserted into.
- If the bucket has space for the new record, insert the record and we are done.
- If the bucket is full, then we need to split it into two buckets. To split the bucket, increment its local depth by 1 and create two new buckets with the same local depth. Then, redistribute the records in the original bucket into the two new buckets based on the next bit in their hash values. Update the directory accordingly to point to the new buckets.
- If the global depth of the directory is less than or equal to the local depth of the bucket, then we need to increase the global depth of the directory. To do this, we double the number of entries in the directory and copy each entry twice. The first entry points to the same bucket as before, and the second entry points to a new bucket with the same local depth as the first bucket. Update the directory to point to the new buckets.

This process of splitting and doubling the directory can be repeated indefinitely as needed to handle a growing number of records. When a record needs to be deleted, we simply remove it from the appropriate bucket. If the bucket becomes empty after the deletion, we can merge it with its sibling bucket and update the directory accordingly.

### Different cases to consider

In extendible hashing, there are several cases to consider when performing operations like insertion, deletion, and searching. Here are some common cases:

1. **If local depth equals global depth:** In this case, no split is required, and the record is inserted into the appropriate bucket.
2. **If local depth is less than global depth:** In this case, the appropriate bucket is identified based on the hash value, and the record is inserted into the bucket. The bucket is then checked to see if it has reached its maximum capacity. If it has, the bucket is split into two new buckets, and the local depth is increased by 1.
3. **If local depth is greater than global depth:** This should not happen in a correctly implemented extendible hashing scheme. However, if it does happen, it means that the directory has not been updated correctly, and the scheme needs to be reorganized to correct the problem.
4. **If a record needs to be deleted:** The record is located using the hash function, and then it is removed from the appropriate bucket. If the bucket becomes empty after the deletion, the bucket is removed, and the local depth is decreased by 1 if it is safe to do so.
5. **If the directory needs to be expanded:** If all the buckets for a particular hash prefix are full, and the local depth is equal to the global depth, then the directory needs to be expanded. This involves creating a new directory that has twice the number of entries as the current directory, and copying the appropriate entries from the old directory to the new one.

Overall, extendible hashing provides a dynamic and efficient way to manage large datasets in a database. By using a hash function to bin records into buckets, extendible hashing enables fast searches and insertions, while also allowing for easy scalability.

### In my words:

It basically takes the hashed value of the elements and then tries to bin the elements based on the last digits of the hashed values of the elements. If the bin runs out of space then it will take one more digit to split the bin and accommodate it. 

Unnecessary binning is not done, so if there is some bin where there is space then it won't be split and even after other bins split, then multiple keys which were pointing to this bin earlier, will keep pointing to this bin.


