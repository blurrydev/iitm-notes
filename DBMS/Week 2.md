# Lecture 1: Introduction to Relational Model - I

#### Attributes

- **Attribute:** Column (in terms of table)
- **Domain of an attribute:** Set of values allowed for each attribute.
- Attribute values are normally *atomic* in nature.
- **Instance:** Row (in terms of table)

#### Relational Schema and instances

- If $A_1$, $A_2$,..., $A_n$ are attributes
- $R$ = ($A_1$, $A_2$,..., $A_n$ ) is a relation schema
- Given sets $D_1$, $D_2$, ... , $D_n$ 
	- Relation is a set of n tuples ($a_1$, $a_2$, ... , $a_n$) where $a_i$ $\in$ $D_i$
- Relations are *unordered* with *unique tuples*

#### Keys

- A **superkey** is a set of attributes in a relation (table in database) that can uniquely identify a tuple (row).
- A **candidate key** is a minimal superkey, meaning it is a superkey with the least number of attributes that can still uniquely identify a tuple. There can be multiple candidate keys in a relation.
- A **primary key** is one of the candidate keys that is chosen by the database designer to be the main means of identifying tuples in the relation. The primary key is used to enforce the entity integrity of the relation, meaning that each tuple in the relation must have a unique primary key value.
- A **secondary key** is *candidate key* - *primary key*.
- A **surrogate key** is an artificial key which is not a natural part of the database but is created artificially.
- A **foreign key** is a key which is derived from another relation.
- A **compound key** is a when we mix two or more attributes to uniquely identify an attribute.

#### Relational Query Language

- **Procedural programming:** Requires the programmer to tell the computer what to do.
- **Declarative Programming:** Requires the programmer to declare what they want using the relationship that holds between various entities.
- **Pure relational query languages:**
	- Relational Algebra
	- Tuple relational calculus
	- Domain relational calculus

# Lecture 2: Introduction to Relational Model - II

#### Relational Operators

##### Select
- Symbol: $\sigma$
- Function: It takes out *rows* based on the given condition

##### Project
- Symbol: $\pi$ 
- Function: It takes out *columns*
> When it takes out the columns then the resulting schema will eliminate duplicate tuples

##### Union
- Symbol: $\cup$ 
- Function: If two relations have *identical attributes* then we can take their union.
- Number of columns in both tables must be same
> When it created the resulting schema after union then it will eliminate duplicate tuples.

##### Difference
- Symbol: $-$ 
- Function: 
	- Let's say we're doing $r - s$ , this means r but not s.
	- So the resulting relation will have:
		- All tuples of r *except* the ones which are common in both r and s

##### Cartesian Product
- Symbol: $\times$
- Function: Make all possible combinations of the tuples.

##### Natural Join
- Symbol: $\bowtie$ 
- Function: 
	- Makes all possible combinations of tuples *provided*
		- There is at least one common attribute within the relations *and*
			- The combinations are made on of the tuples where the tuples have same value.
- Procedure:
	- Find the common attributes
	- Select a tuple from the first table
	- Check if the common attribute of the selected tuple has identical values in the other table.
	- If so, make possible combinations with them. Else skip it and go to the next tuple from the first table.
	- Do not make combinations of tuples which do not have same value in the common attributes.
> Remove all duplicate tuples from the resulting table

# Lecture 3: Introduction to SQL - I

#### Data Definition Language (DDL)

- It is a language that is used to define or edit the schema.
- Example:
```SQL
CREATE TABLE instructor(
ID char(5),
name varchar(20) not null,
dept_name varchar(20),
salary numeric(8,2),
primary key (ID),
foreign key (dept_name) references department
);
```

> When you use ALTER TABLE to add attribute then it cannot be made not null because the existing instances will have null values for that attribute.


### **Order of SQL clauses:**
- SELECT
- FROM
- GROUP BY
- HAVING
- ORDER BY


# Lecture 4: Introduction to SQL - II

#### String Operations

- **Percent (%):** It matches any *substring*.

Example: Find the name of all instructors whose name has the value *dar* in it.

```SQL
SELECT name,
FROM instructor,
WHERE name like '%dar%'
```

- **Underscore ( _ ):** It matches any *character*.

Example: Find the name of all instructor whose name has only 5 letters.

```SQL
SELECT name,
FROM instrutor,
WHERE name like '_____'
```

#### Duplicates

> In relational algebra duplicates are not allowed but in SQL duplicates are allowed.

- **Multiset:** In this version of relational algebra we *do not* enforce duplicate removal.
> SQL internally follows multiset


# Lecture 5: Introduction to SQL - III

#### Set Operations

- Two relations can be involved in binary set operations only when they are identical in structure.
- Set Operations and their meanings:
	- **Or:** Union
	- **And:** Intersection
	- **Not in:** Except

How to find highest salary using set operations:
1. Find the salaries which are not highest.
```SQL
SELECT DISTINCT T.salary
FROM instructor as T, instructor as S
WHERE T.salary < S.salary
```
2. Find all the salaries
```SQL
SELECT DISTINCT salary
FROM instructor
```
3. Subtract 2 - 1
```SQL
(SELECT "second query")
EXCEPT
(SELECT "first query")
```

The **Multiset** versions of set operations:
- **Union:** Union all
- **Intersection:** Intersection all
- **Except:** Except all

Suppose a tuple occurs *m times in r* and *n times in s*:
- m + n times in r *union all* s
- min(m,n) times in r *intersect all* s
- max(m,n) times in r *except all* s

