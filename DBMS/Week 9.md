# Indexing

- Indexing is used to speed up access to desired data.

- **Dense** is when there are `n` entries in the index table for `n` entries in the original table.
	- Number of entries in index is equal to the number of entries in the original table.
- **Sparse** is when we make one entry in the index table for each block in the original table.
	- Number of entries in index table is equal to number of blocks in the hard drive.
	- Can only be done when *data is ordered or sorted*.
	- The record which is used as `search key` is called *Anchor record*.
- Each index table has a `key` and a `pointer`.
- Index is always sorted so the time required to search is $log_2$ $n$.

## Types of indices

- **Ordered file:** All data are ordered or sorted.
- **Unordered file:** Data not ordered or sorted.
- **Key:** If data has all unique elements which can be made key.
- **Non Key:** If data has no unique element which can be made key.

![[Pasted image 20230419224745.png]]

There are **three** types of indices:
1. Primary: This is like how we use primary key in DBMS.
2. Clustered: Here we will 
3. Secondary

> - Secondary index can only be made from unordered file
> - Ordered files can create primary or clustered index depending upon if the values are unique or not.

