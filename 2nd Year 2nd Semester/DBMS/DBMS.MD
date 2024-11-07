# [Basics of Functional Dependencies and Normalization for Relational Databases](https://www.tutorialspoint.com/basics-of-functional-dependencies-and-normalization-for-relational-databases)

## Introduction
Functional dependencies and normalization are important concepts in relational database design. A functional dependency occurs when the value of one attribute determines the value of another attribute. Normalization is the process of organizing a database in a way that reduces redundancy and dependency. It is a crucial step in designing an efficient and effective database structure.

## What are functional dependencies?
Functional dependencies are relationships between attributes in a database. They describe how one attribute is dependent on another attribute. For example, consider a database of employee records. The employee's ID number might be functionally dependent on their name because the name determines the ID number. In this case, we would say that the ID number is functionally dependent on the name.

Functional dependencies can be used to design a database in a way that eliminates redundancy and ensures data integrity. For example, consider a database that stores employee records and the departments they work in. If we store the department name for each employee, we might end up with several copies of the same department name.

This would be redundant and would take up unnecessary space in the database. Instead, we can use functional dependencies to store the department name only once and use the employee's ID number to determine which department they work in. This reduces redundancy and makes the database more efficient.

Explore our latest online courses and learn new skills at your own pace. Enroll and become a certified expert to boost your career.

## Why is Normalization Important?
Normalization is the process of organizing a database to reduce redundancy and dependency. It is important because it helps to eliminate data inconsistencies and ensures that the data is stored in a logical and organized way.

For example, consider a database that stores customer information and the products they have purchased. If we store the product names with each customer record, we might end up with several copies of the same product name. This would be redundant and would take up unnecessary space in the database. Instead, we can use normalization to create a separate table for products and store the product names only once. This reduces redundancy and makes the database more efficient.

There are several normal forms that can be used to normalize a database. The most common normal forms are the first, second, and third normal forms.

## First normal form (1NF)
The first normal form (1NF) is a basic level of normalization. To be in 1NF, a table must meet the following criteria −

It must contain only atomic values. An atomic value is a single value that cannot be further broken down. For example, a name is an atomic value, but an address is not because it can be broken down into separate values for the street, city, state, and zip code.

It must not contain repeating groups. A repeating group is a set of values that are repeated within a single record. For example, if a table contains a field for phone numbers, it should not contain multiple phone numbers within the same field. Instead, there should be separate fields for each phone number.

## Second normal form (2NF)
The second normal form (2NF) is a higher level of normalization. To be in 2NF, a table must meet the following criteria −
>> 
> It must be in 1NF.
>
>It must not have any partial dependencies. A partial dependency occurs when a non-key attribute is dependent on only a part of the primary key. For example, consider a table with the following attributes: EmployeeID (primary key), EmployeeName, and DepartmentID. If the DepartmentID is dependent on the EmployeeID, but not on the EmployeeName, there is a partial dependency. To eliminate this dependency, we would create a separate table for departments and store the DepartmentID and DepartmentName in that table.

## Third normal form (3NF)
The third normal form (3NF) is a higher level of normalization. To be in 3NF, a table must meet the following criteria −
>>
> It must be in 2NF.
>
> It must not have any transitive dependencies. A transitive dependency occurs when an attribute is dependent on another attribute that is not the primary key. For example, consider a table with the following attributes: EmployeeID (primary key), EmployeeName, and ManagerID. If the ManagerID is dependent on the EmployeeID, which is the primary key, there is no transitive dependency. However, if the ManagerID is dependent on the EmployeeName, which is not the primary key, there is a transitive dependency. To eliminate this dependency, we would create a separate table for managers and store the ManagerID and ManagerName in that table.

### Real-life Examples
To better understand these concepts, let's look at some real-life examples of functional dependencies and normalization.

### Example 1
Consider a database of customer orders for an online store. The following table stores information about each order −

![Table1](image.png)

In this table, the OrderID is the primary key and the CustomerID and ProductID are foreign keys. The Quantity attribute is dependent on the OrderID, because it determines the quantity of each product in the order.

This table is in 1NF because it contains only atomic values and does not have any repeating groups. However, it is not in 2NF because the Quantity attribute is dependent on the OrderID, which is only a part of the primary key (OrderID, ProductID). To eliminate this partial dependency, we can create a separate table for order details and store the OrderID, ProductID, and Quantity in that table.

![Table2](image-1.png)

### Example 2
Consider a database of employee records for a company. The following table stores information about each employee −

![Table3](image-2.png)

In this table, the EmployeeID is the primary key and the ManagerID and DepartmentID are foreign keys. The ManagerID is dependent on the EmployeeID, because it determines the employee's manager. The DepartmentID is dependent on the ManagerID, because it determines the department the employee works in.

This table is in 2NF because it is in 1NF and does not have any partial dependencies. However, it is not in 3NF because the DepartmentID is dependent on the ManagerID, which is not the primary key. To eliminate this transitive dependency, we can create a separate table for departments and store the DepartmentID and DepartmentName in that table. We can then update the employees table to store the DepartmentID as a foreign key.

![Table4](image-3.png)

### Conclusion:
Functional dependencies and normalization are important concepts in relational database design. They help to eliminate redundancy and ensure data integrity by organizing the database in a logical and efficient way. By understanding these concepts and applying them to your database design, you can create a database that is efficient, effective, and easy to maintain.
