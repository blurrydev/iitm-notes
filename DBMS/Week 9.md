# Indexing

- Indexing is used to speed up access to desired data.

- **Dense** is when there are `n` entries in the index table for `n` entries in the original table.
- **Sparse** is when we make one entry in the index table for each block in the original table.
	- Can only be done when *data is ordered or sorted*.
- Each index table has a `key` and a `pointer`.
- Index is always sorted so the time required to search is $log_2$ $n$.

## Types of indices

- **Ordered file:** All data are ordered or sorted.
- **Unordered file:** Data not ordered or sorted.
- **Key:** If data has all unique elements which can be made key.
- **Non Key:** If data has no unique element which can be made key.

![[Pasted image 20230419224745.png]]