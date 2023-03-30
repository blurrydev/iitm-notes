## Anomalies

1. **An update anomaly** occurs when a change made to one row of a table affects multiple rows, leading to inconsistencies in the data. 
	- For example, suppose you have a table with customer information, and a customer changes their phone number. If their phone number is stored in multiple rows, such as in both an order table and a customer table, updating the phone number in one place may not update it in the other place, leading to inconsistencies.
2. **A delete anomaly** occurs when deleting a row from a table also deletes other unintentional rows or makes the data inconsistent. 
	- For example, suppose you have a table with customer orders and customer information. If a customer cancels their order, deleting the order may also delete the customer's information if the order and customer information are stored in the same table.
3. **An insert anomaly** occurs when inserting new data into a table requires additional data to be inserted that is not currently available.
	- For example, suppose you have a table with customer orders and customer information. If a new customer places an order, but there is no existing information for the customer, you cannot insert the order information without first inserting the customer information. This can lead to a situation where you have incomplete data or a table with missing values.

# Decompositions

Wen we decompose a relation then we will always try to gain the following properties:
	1. [[Week 5#Lossy and lossless decomposition]]
	2.  [[Week 5#Dependency Preserving Decomposition]]

