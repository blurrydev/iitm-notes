# Decomposition

- Decomposition is the process of breaking down a relation `R` into smaller relations `R1` & `R2`.
- This is done to eliminate redundancy and improve data integrity.

#### Lossy and lossless decomposition

The smaller relations that we just created will be naturally joined now.

- It the natural join return the same relation as that other original relation then it is **Lossless**.
	- When decomposing we need to make sure that the common attribute is *a candidate key or a super key of either `R1` or `R2` or `both R1 and R2`*.
- If it is not and return more or less data then it is **Lossy**.


#### Dependency Preserving Decomposition

1.  Identify all functional dependencies (FDs) in the original relation R.
2.  Decompose R into smaller relations using a set of decomposition rules.
3.  For each FD in R, check if it can be derived from the smaller relations created in step 2.
4.  If all the FDs from R can be derived from the smaller relations, then the decomposition preserves the dependencies.

To check if an FD can be derived from the smaller relations, we can follow these steps:

1.  Identify the set of attributes involved in the FD.
2.  Check which smaller relations contain all the attributes involved in the FD.
3.  For each smaller relation containing a subset of the attributes in the FD, compute the closure of that subset within the smaller relation. If the closure includes all the attributes involved in the FD, then the FD can be derived from that relation.
4.  If the FD can be derived from the smaller relations, then the decomposition preserves the dependencies.

If any FDs cannot be derived from the smaller relations, then the decomposition does not preserve the dependencies and it needs to be adjusted accordingly.

# Steps to check Normal Form

1. Find the candidate keys
2. Find the prime attributes
3. Find the non-prime attributes

# First Normal Form

*A table should not contain multivalued attribute.*

Let's say there is a table `Student(roll_number, name, course)`

For example let's say there a student table that contains course information of students and someone has taken two courses so the `course` attribute has two values, then the table is not in 1NF.

#### How to convert it into 1NF?

###### Method 1:
- Write one course in one row along with other information of the student.
- Now the roll number will be repeating so we will have to change the primary key to the combination of the first prior primary key (`roll_number`) and recently split attribute (`course`) i.e. a compound primary key.

###### Method 2:
- Create a new column which will accept the additional course in it.
- It should be nullable so students who doesn't have additional courses can have the additional course column as `null`.
- In this case we can have a simple primary key i.e the previous primary key (`roll_number`).
- Issue with this method is that let's say there is one student who has taken n courses while others have taken just 1 then others will have more `null` values in the record which is not so good.

###### Method 3:
- This method is like breaking up the table of [[#Method 1:]] into a base table and a referencing table.
- The base table will just contain the `roll_number` and `name`. Primary key will be just the original primary key (`roll_number`)
- The referencing table will contain `roll_number` and `course`. Primary key will be compound of both `roll_number` and `course`.

# Functional Dependency

Let's take the expression $x \to y$ 
- Here we say that $x$ determines $y$
- $x$ here is the *determinant*
- $y$ is the *dependent*

Now let's take a scenario where $sid \to sname$ 
- We see that there are two entries with $sname$ = Rahul
- We get confused if both rows are indicating to two different Rahuls or same.
- So we will now go back to our determinant $sid$ and check.
- If we see that the $sid$ are different for both then it'll mean that the rows are indicating to two different Rahuls else both are indicating to same person and the value was somehow repeated.

#### Valid & invalid

- A **valid functional dependency** is one where the determinant uniquely determines the dependent attribute(s) in a relation.
- An **invalid functional dependency** is one where the determinant does not uniquely determine the dependent attribute(s) or violates transitivity.

#### Trivial and Non-trivial 
 - A **trivial functional dependency** is when the dependent is a subset of determinant, i.e. 
	 - $y \subseteq x$
	 - $x \cap y$ $\ne \phi$ 
	 - Since $y$ is a subset of $x$, therefore this is *always valid*.

- A non trivial functional dependency is when:
	- $x \cap y$ $= \phi$
	- Here the functional dependencies are *not always valid*.

#### Properties

^0718b2

- **Reflexivity:** *Trivial FD*, If $y$ is a subset of $x$ then $x \to y$.
- **Augmentation:** If $x \to y$ then $xz \to yz$
- **Transitive:** If $x \to y$ & $y \to z$  then $x \to z$.
- **Union:** If $x \to y$ & $x \to z$ then $x \to yz$.
- **Decomposition:** *Reverse of Union*. If $x \to yz$ then $x \to y$ & $x \to z$.
- **Pseudo-transitivity:** If $x \to y$ and $wy \to z$ then $wx \to z$.
- **Composition:** If $x \to y$ & $z \to w$ then $xz \to yw$.

#### Keys
- **Superkey:** `K` is a superkey in relation `R` iff $K  \to R$.
- **Candidate Key:** A superkey but with minimal attribute. 
	- K is a candidate key of relation R iff
		- $K \to R$
		- for *no* $\alpha \subseteq K$, $\alpha \to R$

# Second Normal Form

Using 2NF we want to make sure that there is no partial dependency in the relation.

- A table should be in [[#First Normal Form]]
- All the non-prime attributes should be fully functionally dependent on the candidate key.

> - **Non-prime attribute:** Attributes which are not a part of the candidate key.
> - Fully Functionally dependent: There should not be any partial dependency.
> - **Partial Dependency:** If any of the non-prime attribute is determined by a part of the candidate key.

Let's say there is a table `Store(customerID, storeID, location)` 
Here `customerID, storeID` are the *candidate keys* so `location` is the *non-prime attribute*.

Now if `location` is dependent on `storeID` and not `customerID` then it is partially dependent.
To  solve this we will break the table into two such that there is *not partial dependency* in any of the tables.
- The first table will be `Table1(customerID, storeID)`. Here there is not partial dependency since both are composite key which make up the candidate key.
- The second table will be `Table2(storeID, location)`. Here there is no partial dependency since only `storeID` is the candidate key and *we know from before* that `location` is dependent on `storeID`.

#### Steps to check for 2NF

^2799f3

1. First finish [[#Steps to check Normal Form]]
2. Now check if any proper subset of the candidate key is determining any non-prime attribute using the given functional dependencies.
3. If there is any such functional dependency then the relation is **not in 2NF**.

# Third Normal Form

Before we begin, checkout *Transitive Property* from [[#^0718b2]]

- Using 3NF we want to make sure that a *candidate key is directly determining a non-prime attribute* **instead of** *using transitive dependency to indirectly determine it*.
- This is why we want to make sure that **non-prime attributes do not determine non-prime attributes**.

#### Steps to check for 3NF

^0f468b

1. First finish [[#^2799f3]]
2. Then check if any non-prime attribute is determining any non-prime attribute.
3. If so then the relation is **not in 3NF**.

# Boyce Codd Normal Form (BCNF)

This is considered as a special case of [[#Third Normal Form]]

**Why special case?**
Because this is almost same as 3NF but here we will have to make sure that *all functional dependencies have a Candidate key in their LHS*.

In other words, *only candidate keys (and superkeys) are allowed to determine attributes*.

#### Steps to check BCNF
1. First finish [[#^0f468b]]
2. For each functional dependency check if *LHS is a candidate key or a superkey*.
3. If not then the relation is not in BCNF

# Minimal Cover

Main aim is to remove redundant FDs

1. Break all FD such that the RHS has only one attribute.
2. Now we will find out redundant FDs.
	1. Take one FD and pretend as if it doesn't exist.
	2. Now use the rest FDs find out the closure of the LHS of the excluded FD.
	3. If the closure contains the RHS of the excluded FD then this excluded FD will be considered *redundant* and should be removed.
	4. If not then it is not redundant and should not be removed.
	5. Now repeat the same with other FDs
3. Now we will remove redundant attributes from the LHS of the FDs which have more than 1 attributes.
	1. Take FDs with 2 or more attributes on the LHS. ($AB \to C$)
	2. Now take one attribute from the LHS and find it's closure. ($A^+$)
	3. If the closure contains other LHS attributes ($A^+ = {B}$) then it ($A$) is redundant attribute and can be removed. Why? Because of transitive property.
	4. Else it is non redundant.

# Equivalence of Functional Dependencies

1.  Two sets of functional dependencies are equivalent if they have the same closure, that is, they imply the same set of dependencies.
2.  To check the equivalence of two sets of functional dependencies, we can use the following algorithm: 
	1. Find the closure of each set of dependencies. 
	2. Compare the closures to see if they are the same.
3.  The closure of a set of dependencies is the set of all functional dependencies that can be derived from the original set using the Armstrong's axioms.
4.  The Armstrong's axioms include reflexivity, augmentation, and transitivity.
5.  To find the closure of a set of dependencies, we can use an algorithm that consists of the following steps: 
	1. Start with the given set of dependencies. 
	2. Apply the reflexivity axiom to add any missing dependencies that have the same attributes on both sides. 
	3. Apply the augmentation axiom to add any missing dependencies that have a subset of attributes on the left-hand side and a superset of attributes on the right-hand side. 
	4. Apply the transitivity axiom to add any missing dependencies that can be derived from the existing dependencies using transitivity. 
	5. Repeat steps b, c, and d until no more changes occur.
6.  If the closures of the two sets of dependencies are the same, then the two sets are equivalent.
7.  If the closures are different, then the two sets are not equivalent.