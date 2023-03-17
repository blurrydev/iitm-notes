# Lecture 1: Why DBMS? I

### Data Management

- Storage
- Retrieval
- Transactions
- Audit
- Archival

Database can be both Physical and Electronic.

- Physical data management is formally called *book keeping*
- Apple introduced Vici calc in 1979 which is like the forefather of spreadsheets.

### Electronic Data Management Parameters

- Durability
- Scalability
- Security
- Retrieval
- Ease of use
- Consistency
- Efficiency
- Cost

### Book keeping

**Problems with book keeping:**
- Durability
- Scalability
- Security
- Retrieval
- Consistency

*Solution is Spreadsheet apps like Google sheets.*

### Why not filesystems?

Lack of efficiency in meeting growing needs.


# Lecture 2: Why DBMS? II

**When we compare between Python and SQL to handle files we get get the following advantages:** 

**Python:**
- Python has more capacity in terms of performing more **arithmetic operations** compared to that of SQL
- Python has **low cost** in terms of hardware, software and human resources as compared to SQL

**SQL:**
- SQL is **more scalable** as compared to python when it comes to handle large data.
- SQL's **time of execution** is very less (*milliseconds*) compared to Python's (*Seconds*)
- **Data persistence** is ensured in SQL.
- SQL is more **robust**
- SQL has **more security** with various levels of access.
- **Programmer's Productivity** is ensured in SQL compared to python where we need to write very long codes for simple tasks.

# Lecture 3: Introduction to DBMS I

### Levels of Abstraction

- **Physical Level:** Describes how data is stored.
- **Logical Level:** Describes data stored in the database and the relationships between the data fields. *For Programmers or DB Administrators*
- **View Level:** Shows information in a derived form. It does not show all the information. *Used by applications.*

### Schema and Instances

- **Schema:** It is the way data is organized.
	- **Logical Schema:** Corresponds to the logical level of abstraction, i.e. how we will describe a relationship in the database.
	- **Physical Schema:** Corresponds to the physical level of abstraction, i.e. overall physical structure of the database.
- **Instances:** Actual value of the data.

- **Physical Data Independence:** This concept says that we should design the schema in such a way that *if we change the physical level of schema then it should not affect the logical schema and view level*.

### Data Definition Language (DDL)

- It is used to **define** the database schema.
- DDL compiler generates a set of table templates and stores it in *data dictionary*.
- Data dictionary contains the metadata about the database.

### Data Manipulation Language (DML)

- It is used to **manipulate** the data.
- It is also known as *Query language*.
- Two classes of language:
	- **Pure:** Used for proving properties about computational power and optimizations.
		- Relational Algebra
		- Tuple Relational Calculus
		- Domain Relational Calculus
	- **Commercial:** used for commercial systems.
		- SQL
### Database Design

- **Logical Design:** Deciding on the good schema for the database.
- **Physical Schema:** Deciding on the physical design of the database.

# Lecture 4: Introduction to DBMS II

### Database Engine

It has three components:
- **Storage Manager:** Store the entire data of the database.
	- It has two responsibilities:
		- Interact with the OS file manager
		- Efficient storing, retrieving and updating data
- **Query Processing:** Query the stored data.
	- Has three components:
		- **Parsing and translation:** We need a way to understand the SQL (*Parsing*) and then convert it into relational algebra expression (*Translation*).
		- **Optimization:** Find the solution in optimal number of steps.
		- **Evaluation:** 
- **Transactional Manager:** It is a collection of operation that performs a single logical function in a database application.
	- **Transaction-management component:** It ensures that database remains in consistent state despite system failures and transaction failure.
	- **Concurrency-control manager:** Controls interaction among concurrent transaction to ensure the consistency of the database.

