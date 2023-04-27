# Transactions

- Transaction is a set of operations used to perform a set of logical work.
- It generally represents a change in database.
- In transaction we perform two operations:
	1. **Read** : We cannot write data if we don't read it.
	2. **Write** : Write the data in RAM

## Transaction Control Language

1. **COMMIT** : Writing the data in database
2. **SAVEPOINT** : A check point like game where rollback will start from.
3. **ROLLBACK** : To rollback changes.
4. **SET TRANSACTION** : Places a name on the transaction.

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

> Let's say there are two transactions going on parallelly $T_1$ and $T_2$ and if $T_1$ is working on an object $A$ then $T_2$ can only read $A$ **but not do anything else** unless $T_1$ commits.

# Serializability

- Serializability is the process of converting a parallel schedule into a serial schedule.
- The whole idea is to find a clone of the parallel schedule which is in serial and is equivalent to the  parallel schedule.

There are two types of serializable:

1. **Conflict Serializable** 
2. **View Serializable** 

## Conflict Equivalent

### Rules:
1. We can swap the heights of the non conflict pairs.
2. We cannot swap the heights if the conflict pairs in both transactions.

## Conflict Serializability

1. Create a precedence graph with each transaction as a node.
2. Draw edges between nodes which have a conflict.
	1. `R - W`
	2. `W - R` 
	3. `W -W`
3. Now you go to each operation from all transactions, follow the height, and look for it's conflict 
4. If you find a conflict in other transaction then draw an edge as mentioned in step 2.
5. After we go through all the operations then check if the final precedence graph has any loops.
6. Incase *there are loops* then the transaction is *we can't say if it's serializable or not*, else it is.

### How to serialize the schedule

1. From the above precedence graph look for the node which has indegree 0
2. It will be the first transaction
3. Then dismiss that node and all it's edges. 
4. Now again look for the node which has indegree 0
5. Repeat the same thing until all nodes are dismissed.

>If none of the nodes has indegree 0 then there is a cycle in the graph and it's not serializable.


> Cascading anything means that when one action triggers another action. It may be rollback or anything else

# Deadlock Prevention 

## Wait and Die

Let's take a scenario that $T_i$ is requesting data item which is currently held by $T_j$

Now, if $T_i$ is *older*, i.e. has smaller timestamp, then it will **wait**.
Else, if the transaction is newer, i.e. has bigger timestamp, then it will **rollback (die)**.

## Wound and Wait

Let's consider the same scenario as above,

Now, if $T_i$ is older then it will kill the current transaction $T_j$ and acquire the resource.
Else, if the transaction is newer then it will wait for the older transaction to release the resource.

# Locking Protocols

## Shared-Exclusive Locking Protocol

- **Shared Lock (S):** Only read is allowed.
- **Exclusive Lock (X):** Both read and write is allowed.

Here is a compatibility table for shared lock and exclusive lock:

|            | S (shared) lock | X (exclusive) lock |
|------------|----------------|--------------------|
| S (shared)  | Yes            | No                 |
| X (exclusive) | No             | No                 |

In this table, "Yes" indicates that the lock types are compatible and can be granted simultaneously, while "No" indicates that the lock types are incompatible and one transaction must wait for the other to release its lock before it can proceed. 

For example, if a transaction holds a shared lock on a resource, another transaction can also acquire a shared lock on the same resource without blocking. However, if a transaction holds an exclusive lock on a resource, no other transaction can acquire a shared or exclusive lock on the same resource until the lock is released.

### Disadvantages

1. Not sufficient to produce only serializable schedule.
2. May not free from recoverability
3. May not free from deadlock
4. May not free from starvation


## 2 Phase Locking (2PL)

This is basically the modification of the above locking protocol just to overcome the disadvantages that we discussed earlier.

There are two phases:

1. **Growing Phase:** Here we just keep acquiring locks without releasing them.
2. **Shrinking Phase:** Here we keep releasing locks without acquiring any.

>Any transaction which follows the 2PL protocol, it has to be **serializable**.

- **Lock Point:** The place where the last locking is done or the first unlocking is done.

#### How to find the serializability?

The serializability will go along with the lock point preference. The transaction whose lock point comes first will take place first followed by the next and so on.

#### Disadvantages

- May not free from irrecoverablity
- Not free from deadlocks
- Not free from starvation
- Not free from cascading rollback

### Strict and Rigorous 2PL

To over come the drawback that we discussed above we modify 2PL further.

- **Strict 2PL:** It says that all *exclusive locks* must not be unlocked *until commit or abort*.
- **Rigorous 2PL:** It says that *all locks (shared and exclusive)* must not be unlocked *until commit or abort*.

# Time Stamp Ordering Protocol

- **Timestamp:** A unique value is assigned to every transaction. Generally higher values are given to younger transactions. Also denoted with $TS (T_i)$.
- **Read Timestamp (RTS):** The last transaction which performed read operation successfully.
- **Write Timestamp (WTS):** The last transaction which performed write operation successfully.
- Both the RTS and WTS vary from variable to variable.

## Rules

- We will assume that the older transaction will always commit first.
- If there is a newer transaction which is performing read or write operation and then an older transaction wants to perform an operation then *we will not allow it*. 
- If it does then we will rollback the transaction of the older transaction.

1. **Transaction $T_i$ issues a Read (A) operation:**
	- If, $WTS(A)$ > $TS$($T_i$)
		- Rollback $T_i$
	- Else, Execute $R(A)$ 
		- Set $RTS(A)$ = $max (RTS(A), TS(T_i))$
2. **Transaction $T_i$ issues a Write (A) operation:**
	- If $RTS(A)$ > $TS(T_i)$
		- Rollback $T_i$
	- Elif $WTS(A)$ > $TS(T_i)$
		- Rollback $T_i$
	- Else execute Write (A) operation
		- Set $WTS(A)$ = $TS(T_i)$

>We basically check for the conflict pairs to make sure that newer transactions are not working on the same object.

