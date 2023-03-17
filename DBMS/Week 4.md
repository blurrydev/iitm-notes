# Lecture 1: Formal Relational Query Language I

There are 2 formal relational query languages:
1. Relational Algebra; Procedural & Algebra based.
2. Tuple relational calculus (TRC): Non procedural & predicate based.
3. Domain relational calculus (DRC): Non procedural & predicate based.

### Relational Algebra

[[Week 2#Relational Operators]]

#### Projection
- It is always used at the last of the expression
- It just fetches the column
- Eg: Select column 'roll_no' from table students
	- $\pi_{roll\_no}$ (students)

#### Selection
- Selects row based on the given condition.
- Eg: Select roll_no from students where sec is A
	- $\sigma_{sec = A}$(students)
	- On this we will apply project to get the column roll_no

#### Cross Join
- There must be at least one common attribute (column) between the tables to be cross joined.

#### Set difference
- $A - B$  means $A$ but not $B$
- Can also be written as $A \cap B'$ 
- Number of columns and data type must be same
- Not commutative

#### Union

^da2738

- Number of columns should same in both tables
- Domain of every column should be same i.e. data type should be same in every tuple.
- Column name will always be the column names of the left table in the expression.

#### Intersection
- Same as set theory
- The conditions are same as [[#^da2738]]
- $r \cap s$ = $r - (r - s)$

#### Division
- It is a derived operator, i.e. it doesn't exist by itself but we use other operators to derive it.
- Use this method for queries that ask for *for all*, *every*.
	- Eg: Find the roll_no of students who are enrolled in *every* course.

##### Notation
- / 
- $A(x,y)$ / $B(y)$
	- Here the numerator will be the one from which we need to extract the final result.
	- And the denominator will be the one which will help the numerator to extract the result.
	
For example, let's consider two relations R and S, where R has attributes A, B, and C, and S has attributes B and C. The division operator can be expressed using the following notation:

R ÷ S

The result of the division operator R ÷ S is a relation that contains all the tuples from relation R that are associated with every tuple in relation S.

#### Other Notations

^323445

-   **and:** $\wedge$
-   **or: $\vee$**
-   **not:** $\neg$ 

# Lecture 2: Formal Relational Query Language II

### Tuple Relational Calculus

^ee0dea

- It is a part of the relational calculus but unlike relational calculus, TRC only focuses on tuples.
- It scans through all the tuples and selects the tuples which match the condition.
- It is a non procedural query language, i.e. we tell it what we want but we don't tell it how to achieve the result.

#### Operations
- TRC has the same operators like Relational Calculus. [[#^323445]]
- Apart from the above, it also uses *quantifiers*:
	- $\exists$ $\to$ there exists
	- $\forall$ $\to$ for all

### Domain Relational Calculus
- It is similar to TRC but instead of tuples, we will focus on attributes (columns).
- All conditions are same as [[#^ee0dea]]

# Entity Relationship Model

- **Entity:** Anything which is an object and which has a physical existence.
	- *Shape:* Rectangle
- **Attribute:** Characteristics of the entity.
	- *Shape:* Eclipse
- **Relationship:** Relation between different entities.
	- *Shape:* Diamond

### Types of attributes

- **Single Valued Attribute:** This attribute cannot have more than one value.
	- *Shape:* Eclipse
- **Multivalued Attribute:** This attribute can one or more values.
	- *Shape:* Double Eclipse

- **Simple Attribute:** This cannot be divided any further.
	- Example: Age
- **Composite Attribute:** This is made of multiple simple attribute and can be further divided.
	- Example: Name can be divided into first name and last name

- **Stored Attribute:** This attribute is stored as it is instead of deriving it from other attributes.
	- Example: DOB
- **Derived Attribute:** This attribute is derived from other attributes.
	- Example: Age is derived from DOB
	- *Shape:* Dotted eclipse

- **Key Attribute:** This attribute is used to identify a tuple uniquely like primary key.
	- *Shape:* Underline
- **Non key:** This can be unique or not.

#### Weak entity set

- A weak entity set has a partial key, which is a combination of its own attributes and the primary key of its identifying entity set.
- A partial key is underlined with a dashed line to indicate that it is not a full primary key.
- A weak entity set is depicted as a double rectangle, with its name underlined to indicate the partial key.
- An identifying relationship connects the weak entity set to its identifying entity set.
- The identifying relationship is represented by a diamond shape, which connects the weak entity set to its identifying entity set.
- The relationship line connecting the identifying entity set to the weak entity set is labeled with the word "identifying" to indicate that this is an identifying relationship.
- Total participation indicates that every instance of the identifying entity set must be associated with at least one instance of the weak entity set. This is represented in the ER diagram by a double line connecting the identifying entity set to the identifying relationship diamond.


#### Types of relationships:

###### One to One

- One-to-one relationship means that one record in one table corresponds to exactly one record in another table.
- To create a relationship table based on a one-to-one relationship, you need to identify the two tables that have this relationship and create a new table that connects them.
- The relationship table should contain a foreign key that references the primary key of the related table. For this check which attribute has unique values and assign it primary key. If both have unique values then you can choose either.
- When populating the relationship table, you need to make sure that each record in the related tables has a corresponding record in the relationship table.
- One way to do this is to add the foreign key value from the related table to the relationship table for each record.
- You can use the relationship table to retrieve information about the related records using simple queries that reference the foreign key and the primary key values.
- It's important to ensure data integrity by enforcing constraints on the relationship table, such as preventing the insertion of duplicate foreign keys or null values.

###### One to Many

- The *attribute of the the relationship* is called **descriptive attribute**.

- In a one-to-many relationship, one record in one table can correspond to one or many records in another table.
- To create a relationship table based on a one-to-many relationship, you need to identify the two tables that have this relationship and create a new table that connects them.
- The relationship table should contain foreign keys that reference the primary keys of each of the related tables.
- The primary key in the "many" side of the relationship should be added to the relationship table.
- When populating the relationship table, you need to make sure that each record in the related tables has a corresponding record in the relationship table.
- One way to do this is to add the primary key value from the "many" side of the relationship and the foreign key value from the "one" side to the relationship table for each related record.

###### Many to Many
- Many-to-many relationship means that many records in one table can correspond to many records in another table.
- To create a relationship table based on a many-to-many relationship, you need to identify the two tables that have this relationship and create a new table that connects them.
- The relationship table should contain foreign keys that reference the primary keys of each of the related tables.
- The primary key in the relationship table should be a combination of the foreign keys from both tables.
- When populating the relationship table, you need to make sure that each combination of related records has a corresponding record in the relationship table.
- One way to do this is to add a record to the relationship table for each combination of related records, with the primary key value being a combination of the foreign key values.

