#SQL

1. DBMS
    1. Database Management System is a system software responsible for creation, retrieval, updation and manipulation of database
2. RDBMS
    1. Relational Database Management System stores data in the form of collection of tables and relation can be defined between the common fields of these tables
3. SQL
    1. Structured Query language. 
    2. It is standard language for relational database management system
4. Constraints in SQL
    1. NOT NULL —> Restricts NULL value from being interred into a column
    2. CHECK —> Verifies that all values in a field satisfy a condition
    3. DEFAULT —> Automatically assigns a default value if no value has been specified for the field
    4. UNIQUE —> Ensures unique values to be inserted into the field
    5. INDEX —> Indexes a field providing faster retrieval of records
    6. PRIMARY KEY —> Uniquely identifies each record in a table
    7. FOREIGN KEY —> Ensures referential integrity for a record in another table
5. Joins
    1. (Inner) join
        1. Retrieves record that have matching values in both tables involved in the join.
    2. Left (outer) join 
        1. Retrieves all the records from the left and the matched records from the right
    3. Right (outer) join
        1. Retrieves all records from right and matched records on the left table
    4. Full (outer) join
        1. Retrieves all records where there is a match in either left or right table
    5. Self join
        1. Is a case of regular join where a table is joined to itself based on some relation between its own columns
        2. Uses the inner join or left join clause and a table alias is used to assign different names to the table within the query
    6. Cross join
        1. Can be defined as a Cartesian product of two tables included in the join
        2. The table after join contains the same number of rows as in the cross-product of number of rows in the two tables
        3. If a where class is used in cross join then the query will work line Inner join
6. Index
    1. A database index is a data structure that provides quick lookup of data in a column or columns of a table
    2. It enhances speed of operations accessing data from a database table at the cost of additional writes and memory to maintain index data structure
    3. Types
        1. Unique and non unique index
            1. Unique indexes are indexes that help maintain data integrity by ensuring that no two rows of data in a table have identical key values.
            2. Once a unique index has been defined for a table, uniqueness is enforced whenever keys are added or changed within index
            3. Non-unique index are not used to enforce constraints on the tables with which they are associated. Instead, non-unique indexes are used solely to improve query performance by maintaining a sorted order of data values that are used frequently
        2. Clustered and non clustered index
            1. Clustered indexes are indexes whose order of the rows in the database correspond to the order of the rows in the index. This is why only one clustered index exists in a given table
            2. Multiple non clustered index can exist in the table
            3. Difference between the two is that the database manager attempts to keep the data in the database in the same order as the corresponding keys appear in the clustered index
            4. Clustering index can improve the performance of most query operations because they provide a linear-access path to data stored in database
            5. Clustered index modifies the way records are stored in database based on the indexed column.
            6. Non clustered index creates a separate entity within the table which references the original table
            7. Clustered index is used for easy and speedy. Retrieval of data from the database, whereas, fetching records from the non-clustered index is relatively slower
7. Data integrity
    1. It is the assurance of accuracy and consistency of data over its entire life cycle and is a critical aspect to the design, implementation and usage of any system which stores,, processes or retrieves data.
8. Subquery
    1. Subquery is a query within a query known as nested or inner query
    2. It is used to restrict or enhance the data to be queried by the main query, thus restricting or enhancing the output of the main query respectively
    3. Types
        1. Correlalted subquery cannot be considered as an independent query but it can refer the column in a table listed in the from of main query
        2. Non correlated subquery can be considered as an independent query and the output of subquery is substituted in the main query 
9. Clauses
    1. WHERE —> Used to filter records that are necessary based on specific conditions
    2. ORDER By —> used to sort the records based on some field in ascending or descending order
    3. GROUP BY —> used to group records with identical data and can be used in conjunction with some aggregation functions to produce the summarised results from the database
    4. HAVING —> used to filter records in combination with the GROUP BY clause. It is different from WHERE, since WHERE clause cannot filter aggregated records
10. Union
    1. UNION operator combines and returns the result set retrieved by two or more SELECT statements
11. MINUS
    1. Used to remove duplicates from the result set obtained by the second SELECT query from the result set obtained by the first SELECT query and return the filtered results from the first
12. INTERSECT
    1. Combines the result set fetched by the two selects statements where records from one match the other and returns the intersections of result-sets
13. Cursor
    1. Cursor is a control structure that allows for traversal of records in a database
    2. In addition, facilitates processing after traversal, such as retrieval, addition and deletion of database records
    3. They can be viewed as a pointer to one row in a set of rows
    4. Working
        1. DECLARE a cursor after any variable declaration. The cursor declaration must always be associated with a SELECT statement
        2. Open cursor to initialise the result set. The OPEN statement must be called before fetching rows from the result set
        3. FETCH statement to retrieve and move to the next row in result set
        4. Call the CLOSE statement to deactivate the cursor
        5. Finally use the DEALLOCATE statement to delete the cursor definition and release the associated resources
14. View
    1. A view in SQL is a virtual table based on the result set of an SQL statement
    2. A view contains rows and columns, just like a real table
    3. The fields in a view are fields from one or more real tables in database
    4. Note
        1. Multiple views can be created on one table
        2. Views can be defined as read-only or updatable
        3. Views can be indexed for better performance
        4. Insert, update, delete can be done on an updatable view
15. Normalization
    1. Represents the way of organising  structured data in the database efficiently. It includes creation of tables establishing relationships between them, and defining rules for those relationships. 
    2. Inconsistency and redundancy can be kept in check based on theses rules, hence adding flexibility to database
    3. Forms
        1. First Normal form
            1. A relation is in first normal form if every attribute in that relation is a single valued attribute.
            2. If a relation contains composite or multi valued attribute, it violated the first normal form
        2. Second normal form
            1. A relation is in second normal form if it satisfies the conditions for first normal form and does not contain any particular dependency.
            2. A relation in 2NF has no partial dependency I.e. it has no prime attribute that depends on any proper subset of any candidate of the table
            3. Often specifying a single column primary key is the solution to the problem
        3. Third normal form
            1. A relation is said to be in 3NF, if it satisfies the conditions for second normal form and there is no transitive dependency between the non prime attributes i.e. all non prime attributes are determined only by the candidate keys of the relation and not by any other no-prime attribute
16. DeNormalisation
    1. Is the inverse process of normalisation
    2. Where normalised schema is converted into a schema which has redundant information
    3. The performance is improved by using redundancy and keeping the redundant data consistent
    4. The reason for performing denormalisation is the overheads produced in query processor by an over normalised structure
17. DELETE
    1. DELETE statement is used to delete rows from a table
18. TRUNCATE
    1. TRUNCATE command is used to delete all the rows from the table and free the space containing the table
19. DROP
    1. DROP command is used to remove an object from database. If you drop a table, all the rows in the table is deleted and the table structure is removed from database
20. Aggregate functions
    1. An aggregate function performs operations on a collection of values to return a single scalar value.
    2. Often used with group by and having clause
    3. AVG()
    4. COUNT()
    5. MIN()
    6. MAX()
    7. SUM()
21. SCALAR function
    1. A scalar function returns a single value based on the input value
    2. LEN()
    3. UCASE()
    4. LCASE()
    5. MID()
22. Collation
    1. Collation refers to a set of rules that determine how data is sorted and compared.
    2. Rules defining the correct character sequence are used to sort the character data
    3. It incorporated options for specifying case-sensitivity, accent marks, kana character types and character width
23. Stored Procedure
    1. A stored procedure is a subroutine available to applications that access a RDBMS.
    2. Such procedures are stored in the database data directory
    3. The sole disadvantage of stored procedure is that it can be executed in the database and occupies more memory in the database server
    4. It also provides a sense of security and functionality as users who can’t access the data directly can be granted access via stored procedure
24. Trigger
    1. Trigger is a database object just like stored procedure.
    2. It is a special kind of stored procedure which fires when an event occurs in database
    3. It is a database object that is bound to a table and is executed automatically
    4. We cannot explicitly call any trigger
    5. Triggers provide data integrity and used to access and check data before and after modification using DDL or DML query
    6. Types
        1. DDL trigger
            1. Data definition language trigger fires in response to a DDL event eg create, alter, drop
        2. DML trigger
            1. Data manipulation language trigger fires in response to a DML event eg insert, update, delete
