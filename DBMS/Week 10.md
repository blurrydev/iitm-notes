# Transactions

- Transaction is a set of operations used to perform a set of logical work.
- It generally represents a change in database.
- In transaction we perform two operations:
	1. Read : We cannot write data if we don't read it.
	2. Write : Write the data in RAM
	3. Commit : Writing the data in database

# ACID Properties

- **Atomicity:** Either all or none.
- **Consistency:** The sum of money right before initiating the transaction and right after finishing a transaction must be the same.
- **Isolation:** We finish one transaction first and then start a new one. Concept of serializability. 
- **Durability:** The changes we make in database should be permanent.

# Transaction States

1. **Passive:** When the transaction is idle and not being in use.
2. **Active:** As soon as we initiate a transaction the transaction is in active state.
3. **Partially Committed:** The step where we have done all our operations but not yet committed in the database.
4. **Committed:** This is the step where we are writing the changes in the database and not just the RAM (temporarily).
5. **Terminated:** This is where the OS deallocates (like RAM, CPU etc.) the resources after the transaction has been committed.
6. **Failed:** If the transaction fails in the *active* state when the transaction is *partially committed*.
7. **Abort:** Due to the property of *atomicity* when any transaction fails we need to abort it and start from beginning by rolling back any thing we did till then.

# Schedule

Schedule tells us the ordering of the execution of multiple transactions.

There are two types of schedules:

1. **Serial:** This says that we will first complete one transaction first before starting another transaction. This is done to maintain *consistency*. While one transaction is in process then other transactions will wait.
	- Advantage: Consistency
	- Disadvantage: Waiting time
2. **Parallel:** In this type of schedule multiple schedules take place parallelly. This is done to avoid the waiting time that we need to bear during serial scheduling.
	- Advantage: Waiting time
	- Disadvantage: Inconsistency

# Read-Write Conflict

- The only operation where there is not conflict is `Read` and `Read` operations.
- Other than that all other operations will create a conflict if we perform them in parallel. 
- We need to make sure that the operations on one object is not interfered with another transaction on the same object. Only `Read` `Read` operations are allowed.
- Other operations are allowed only after the operations in current transactions are committed in the database.
