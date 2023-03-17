# Lecture 1: SQL Examples

- **Pure set:** Does not have duplicates. Eg: UNION
- **Multi set:** Consists of duplicates. Eg. UNION ALL

# Lecture 4: Intermediate SQL 3

#### Transaction

- It is a unit of work.
- **Atomic:** Either fully execute or rollback as if it never happened.
- Isolation from concurrent transactions.
- It begins implicitly but will only end by *Commit* or *rollback*.

#### Cascading Actions in referential integrity

With cascading we can define actions that database engine can take when an user tries to delete or update a key to which an existing foreign key points.

#### Built-in data types in SQL

- **Date:** date '2005-7-27'
- **Time:** time '09:00:30.75'
- **Timestamp:** timestamp '2-5-7-27 09:00:30.75'
- **Interval:** interval '1' day

#### Index creation

```SQL
create index student_id on student(ID)
```

#### User defined Data type

```SQL
create type Dollars as numeric (12,2) final
```

#### Authorizations

- **Read:** Read but no modification
- **Insert:** Insert but no modification
- **Update:** Modification but no deletion
- **Delete:** Deletion

- **Index:** Create and delete index
- **Resources:** Create new relations
- **Alteration:** Add and delete attributes in a relation
- **Drop:** Delete relation

- **Select:** Read or query
- **All privileges:** All privileges


