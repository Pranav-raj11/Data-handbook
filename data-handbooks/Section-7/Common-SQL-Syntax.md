## **Common Syntax**

```{Note}
Key Notes:
- SQL not case sensitive but generally use uppercase for keywords  
- Use ‘--’ to comment lines  
- Ctrl-Shift-Enter to run all  
- Terminate statement with semi-colon  
- Order: SELECT, FROM, WHERE, ORDER BY, LIMIT
```

| Function | Description | Syntax | Example |
| :---- | :---- | :---- | :---- |
| USE | Select database for query | ```sql USE database_name;``` |  |
| Select | Returns the table with the columns specified | SELECT column 1, column2 …  FROM table\_name;    (use \* for all columns) |  |
| AS | Set a column name to something else You can use arithmetic with columns (column\_name \+ 10\) | SELECT column 1 AS ‘new column name’, column2 …  FROM table\_name;   |  |
| WHERE | Used to extract only the records that fulfill the specified condition  | SELECT column 1, column2, … FROM table\_name WHERE condition;  | Select all customers from Mexico: SELECT \* FROM Customers WHERE Country \= ‘Mexico’;  |
| SELECT DISTINCT | Select columns but with no duplicates | SELECT DISTINCT column 1, column2, … FROM table\_name;    (use \* for all columns) For no duplicates |  |
| Operators | Operators used in WHERE clause: \=, \<=\>, BETWEEN (between certain range), LIKE (search for a pattern), IN (specify multiple possible values for a column) | \=, \<=\>, \!=, BETWEEN, LIKE, IN | SELECT \* FROM Products WHERE Price BETWEEN 50 AND 60; SELECT \* FROM Customers WHERE City LIKE 's%'; (starting with s) SELECT \* FROM Customers WHERE City IN ('Paris','London');  |
| AND/OR | Allows for multiple conditions AND has higher precedence | SELECT column 1, column2, … FROM table\_name WHERE condition1 AND condition2 OR Condition3…;  | Eg.  SELECT \* FROM Customers WHERE Country \= 'Spain' AND (CustomerName LIKE 'G%' OR CustomerName LIKE 'R%');  |
| NOT | Used to negate conditions | SELECT column1, column2, ... FROM table\_name WHERE NOT condition; | SELECT \* FROM Customers WHERE CustomerName NOT LIKE 'A%'; |
| IN | The IN operator allows you to specify multiple values in a WHERE clause. | SELECT \*  FROM table\_name  WHERE column\_name IN (value1, value2 …) | SELECT \* FROM Customers WHERE state IN ('VA', 'GA', 'FL') |
| BETWEEN | The BETWEEN operator selects values within a given range. The values can be numbers, text, or dates. | SELECT \*  FROM table\_name  WHERE column\_name BETWEEN *value1* AND *value2* | SELECT \* FROM Customers WHERE birth\_date BETWEEN '1990-1-1' AND'2000-1-1' |
| LIKE | The LIKE operator is used in a WHERE clause to search for a specified pattern in a column. Common pattern notations [here](#like-operator-patterns) | SELECT \*  FROM table\_name  WHERE column\_name LIKE ‘*pattern*’  | SELECT \* FROM customers WHERE address LIKE '%trail%' OR address LIKE '%avenue%'; |
| REGEXP | The LIKE operator is used in a WHERE clause to search for complex specified patterns in a column. Common pattern notations [here](#commonly-used-metacharacters-in-sql-regex) | SELECT \*  FROM table\_name  WHERE column\_name REGEXP ‘*pattern*’ | SELECT \* FROM customers WHERE last\_name REGEXP ‘field|mac|rose’; SELECT \* FROM customers WHERE first\_name REGEXP 'Elka|Ambur'; SELECT \* FROM customers WHERE last\_name REGEXP '(ey|on)$'; SELECT \* FROM customers WHERE last\_name REGEXP '^MY|SE'; SELECT \* FROM customers WHERE last\_name REGEXP 'B\[RU\]'; |
| IS NULL | Checks for null values | SELECT \* FROM table\_name WHERE column\_name IS NULL | SELECT \* FROM orders WHERE shipped\_date IS NULL |
| ORDER BY | Used to sort the result-set in ascending or descending order.  | SELECT \* FROM table\_name ORDER BY column\_name (DESC *optional*) | SELECT \*, quantity \* unit\_price AS total\_price  FROM order\_items WHERE order\_id \= 2 ORDER BY total\_price DESC |
| LIMIT | The LIMIT clause is used to specify the number of records to return. You can use the offset value to skip that number of rows.  | SELECT \* FROM table\_name LIMIT offset, number | SELECT \* FROM customers ORDER BY points DESC LIMIT 3 |
| ‘INNER’ JOIN | The INNER JOIN keyword selects records that have matching values in both tables. Prefix the table with the database name if it’s not in the current database | SELECT column\_name(s) FROM table1 INNER JOIN table2 ON table1.column\_name \= table2.column\_name; |  |
| Self Join | A self join is a regular join, but the table is joined with itself. |  | SELECT e.employee\_id, e.first\_name, m.first\_name AS manager FROM employees e INNER JOIN employees m ON e.reports\_to \= m.employee\_id |
| Joining Multiple Tables | Running a join on multiple datasets | SELECT column\_name(s) FROM table1 INNER JOIN table2 ON table1.column\_name \= table2.column\_name; (INNER) JOIN table3 ON table1.column\_name  \= table3.column\_name | SELECT o.order\_id, o.order\_date, c.first\_name, c.last\_name, os.name AS status FROM orders o JOIN customers c ON o.customer\_id \= c.customer\_id JOIN order\_statuses os ON o.status \= os.order\_status\_id |
| Compound Join Conditions | When you have multiple conditions to join 2 tables.  | SELECT column\_name(s) FROM table1 JOIN table2 ON table1.column\_name \= table2.column\_name AND  table1.column\_name2 \= table2.column\_name2 | SELECT \* FROM order\_items oi JOIN order\_item\_notes oin ON oi.order\_id \= oin.order\_id AND oi.product\_id \= oin\_product\_id |
| Implicit Join | A way to join tables by listing them in the FROM clause, separated by commas, and specifying the join condition in the WHERE clause | SELECT column\_name(s) FROM table1, table2 WHERE table1.column\_name \= table2.column\_name; | SELECT \* FROM orders o, customers c WHERE o.customer\_id \= c.customer\_id |
| OUTER JOIN | Combines data from two or more tables, including all rows from at least one table and matching rows from the other(s) |  |  |
| LEFT JOIN | Returns all records from the left table (table1), and the matching records (if any) from the right table (table2) | SELECT column\_name(s) FROM table1 LEFT JOIN table2 ON table1.column\_name \= table2.column\_name; | SELECT p.product\_id, p.name, oi.quantity FROM  products p LEFT JOIN order\_items oi ON p.product\_id \= oi.product\_id |
| RIGHT JOIN | Returns all records from the right table (table2), and the matching records (if any) from the left table (table1). | SELECT column\_name(s) FROM table1 RIGHT JOIN table2 ON table1.column\_name \= table2.column\_name; |  |
| OUTER Joining Multiple Tables | Running an outer join on multiple datasets | SELECT column\_name(s) FROM table1 LEFT JOIN table2 ON table1.column\_name \= table2.column\_name; LEFT JOIN table3 ON table1.column\_name  \= table3.column\_name | SELECT c.customer\_id, c.first\_name, o.order\_id, sh.name AS shipper FROM  customers c LEFT JOIN orders o ON c.customer\_id \= o.customer\_id LEFT JOIN shippers sh ON o.shipper\_id \= sh.shipper\_id ORDER BY c.customer\_id |
| USING | Simplifies table join operations by letting you specify common columns between tables | SELECT column\_name(s) FROM table1 JOIN table2 USING (column\_name)  | SELECT o.order\_id, c.first\_name, sh.name AS shipper FROM orders o JOIN customers c 	USING (customer\_id) JOIN shippers sh 	USING (shipper\_id) |
| NATURAL JOIN | Performs a join between two tables based on columns that have the same name and compatible data types. This join operation automatically determines the common columns between the tables and removes duplicates in the result set. | SELECT column\_name(s) FROM table1 NATURAL JOIN table2 | SELECT o.order\_id, c.first\_name FROM orders o NATURAL JOIN customers c |
| CROSS JOIN | Returns all records from both tables (table1 and table2) | SELECT column\_name(s) FROM table1 CROSS JOIN table2 | SELECT c.first\_name AS customer, p.name AS product FROM customers c CROSS JOIN products p |
| IMPLICIT CROSS JOIN | A way to join tables by listing them in the FROM clause, separated by commas | SELECT column\_name(s) FROM table1,  table2 | SELECT c.first\_name AS customer, p.name AS product FROM customers c, products p |
| UNION | Used to combine the result-set of two or more queries | SELECT column\_name(s) FROM table1 UNION SELECT column\_name(s) FROM table2; | SELECT order\_id, order\_date, 'Active' AS status FROM orders WHERE order\_date \>= '2019-01-01' UNION SELECT order\_id, order\_date, 'Archived' AS status FROM orders WHERE order\_date \< '2019-01-01' |
| INSERT INTO | Used to insert new records in a table. | 1\. Specify both the column names and the values to be inserted: INSERT INTO table\_name (column1, column2, column3, ...) VALUES (value1, value2, value3, ...); 2\. If you are adding values for all the columns of the table: INSERT INTO table\_name VALUES (value1, value2, value3, ...); | INSERT INTO customers VALUES (DEFAULT, 'John', 'Smith', '1990-01-01', NULL, 'address', 'city', 'CA', DEFAULT) Multiple rows added example:  INSERT INTO shippers (name) VALUES ('Shipper1'),  ('Shipper2'), ('Shipper3') |
| CREATE TABLE | Used to create a new table in a database | CREATE TABLE table\_name (     column1 datatype,     column2 datatype,     column3 datatype,    .... ); | CREATE TABLE invoices\_archived AS SELECT i.invoice\_id, i.number, c.name AS client, i.invoice\_total,  i.payment\_total, invoice\_date, i.payment\_date, i.due\_date FROM invoices i JOIN clients c USING (client\_id) WHERE i.payment\_date IS NOT NULL |
| UPDATE / SET | Used to modify the existing records in a table. | UPDATE table\_name SET column1 \= value1, column2 \= value2, ... WHERE condition; | UPDATE customers SET points \= points \+ 50 WHERE birth\_date \< '1990-01-01' |
| DELETE FROM | Used to delete existing records in a table. | DELETE FROM table\_name WHERE condition; | DELETE FROM invoices WHERE client\_id \= (SELECT \* FROM clients	WHERE name \= 'Myworks') |

### New table

| Function | Description | Syntax | Example |
| :---- | :---- | :---- | :---- |
| USE | Select database for query | ```sql USE database_name; ``` |  |
| Select | Returns the table with the columns specified | ```sql SELECT column1, column2 … FROM table_name; (use * for all columns) ``` |  |
| AS | Set a column name to something else. You can use arithmetic with columns (column_name + 10) | ```sql SELECT column1 AS 'new column name', column2 … FROM table_name; ``` |  |
| WHERE | Used to extract only the records that fulfill the specified condition | ```sql SELECT column1, column2, … FROM table_name WHERE condition; ``` | ```sql SELECT * FROM Customers WHERE Country = 'Mexico'; ``` |
| SELECT DISTINCT | Select columns but with no duplicates | ```sql SELECT DISTINCT column1, column2, … FROM table_name; (use * for all columns) ``` |  |
| Operators | Operators used in WHERE clause: =, <>, BETWEEN (range), LIKE (pattern), IN (multiple values) | ```sql =, <>, !=, BETWEEN, LIKE, IN ``` | ```sql SELECT * FROM Products WHERE Price BETWEEN 50 AND 60; SELECT * FROM Customers WHERE City LIKE 's%'; SELECT * FROM Customers WHERE City IN ('Paris','London'); ``` |
| AND/OR | Allows for multiple conditions. AND has higher precedence | ```sql SELECT column1, column2, … FROM table_name WHERE condition1 AND condition2 OR condition3…; ``` | ```sql SELECT * FROM Customers WHERE Country = 'Spain' AND (CustomerName LIKE 'G%' OR CustomerName LIKE 'R%'); ``` |
| NOT | Used to negate conditions | ```sql SELECT column1, column2, ... FROM table_name WHERE NOT condition; ``` | ```sql SELECT * FROM Customers WHERE CustomerName NOT LIKE 'A%'; ``` |
| IN | Allows specifying multiple values in a WHERE clause | ```sql SELECT * FROM table_name WHERE column_name IN (value1, value2 …); ``` | ```sql SELECT * FROM Customers WHERE state IN ('VA', 'GA', 'FL'); ``` |
| BETWEEN | Selects values within a range | ```sql SELECT * FROM table_name WHERE column_name BETWEEN value1 AND value2; ``` | ```sql SELECT * FROM Customers WHERE birth_date BETWEEN '1990-1-1' AND '2000-1-1'; ``` |
| LIKE | Search for a pattern in a column | ```sql SELECT * FROM table_name WHERE column_name LIKE '*pattern*'; ``` | ```sql SELECT * FROM customers WHERE address LIKE '%trail%' OR address LIKE '%avenue%'; ``` |
| REGEXP | Search for complex patterns in a column | ```sql SELECT * FROM table_name WHERE column_name REGEXP '*pattern*'; ``` | ```sql SELECT * FROM customers WHERE last_name REGEXP 'field|mac|rose'; SELECT * FROM customers WHERE first_name REGEXP 'Elka|Ambur'; SELECT * FROM customers WHERE last_name REGEXP '(ey|on)$'; SELECT * FROM customers WHERE last_name REGEXP '^MY|SE'; SELECT * FROM customers WHERE last_name REGEXP 'B[RU]'; ``` |
| IS NULL | Checks for null values | ```sql SELECT * FROM table_name WHERE column_name IS NULL; ``` | ```sql SELECT * FROM orders WHERE shipped_date IS NULL; ``` |
| ORDER BY | Used to sort the result-set | ```sql SELECT * FROM table_name ORDER BY column_name (DESC optional); ``` | ```sql SELECT *, quantity * unit_price AS total_price FROM order_items WHERE order_id = 2 ORDER BY total_price DESC; ``` |
| LIMIT | Specify number of records to return | ```sql SELECT * FROM table_name LIMIT offset, number; ``` | ```sql SELECT * FROM customers ORDER BY points DESC LIMIT 3; ``` |
| ‘INNER’ JOIN | Select records with matching values in both tables | ```sql SELECT column_name(s) FROM table1 INNER JOIN table2 ON table1.column_name = table2.column_name; ``` |  |
| Self Join | Join a table with itself |  | ```sql SELECT e.employee_id, e.first_name, m.first_name AS manager FROM employees e INNER JOIN employees m ON e.reports_to = m.employee_id; ``` |
| Joining Multiple Tables | Join multiple datasets | ```sql SELECT column_name(s) FROM table1 INNER JOIN table2 ON table1.column_name = table2.column_name; (INNER) JOIN table3 ON table1.column_name = table3.column_name; ``` | ```sql SELECT o.order_id, o.order_date, c.first_name, c.last_name, os.name AS status FROM orders o JOIN customers c ON o.customer_id = c.customer_id JOIN order_statuses os ON o.status = os.order_status_id; ``` |
| Compound Join Conditions | Multiple conditions to join 2 tables | ```sql SELECT column_name(s) FROM table1 JOIN table2 ON table1.column_name = table2.column_name AND table1.column_name2 = table2.column_name2; ``` | ```sql SELECT * FROM order_items oi JOIN order_item_notes oin ON oi.order_id = oin.order_id AND oi.product_id = oin_product_id; ``` |
| Implicit Join | Join tables by listing in FROM clause, using WHERE for condition | ```sql SELECT column_name(s) FROM table1, table2 WHERE table1.column_name = table2.column_name; ``` | ```sql SELECT * FROM orders o, customers c WHERE o.customer_id = c.customer_id; ``` |
| OUTER JOIN | Combines data from two or more tables |  |  |
| LEFT JOIN | Returns all records from left table, matching from right | ```sql SELECT column_name(s) FROM table1 LEFT JOIN table2 ON table1.column_name = table2.column_name; ``` | ```sql SELECT p.product_id, p.name, oi.quantity FROM products p LEFT JOIN order_items oi ON p.product_id = oi.product_id; ``` |
| RIGHT JOIN | Returns all records from right table, matching from left | ```sql SELECT column_name(s) FROM table1 RIGHT JOIN table2 ON table1.column_name = table2.column_name; ``` |  |
| OUTER Joining Multiple Tables | Outer join on multiple datasets | ```sql SELECT column_name(s) FROM table1 LEFT JOIN table2 ON table1.column_name = table2.column_name; LEFT JOIN table3 ON table1.column_name = table3.column_name; ``` | ```sql SELECT c.customer_id, c.first_name, o.order_id, sh.name AS shipper FROM customers c LEFT JOIN orders o ON c.customer_id = o.customer_id LEFT JOIN shippers sh ON o.shipper_id = sh.shipper_id ORDER BY c.customer_id; ``` |
| USING | Simplifies joins by specifying common columns | ```sql SELECT column_name(s) FROM table1 JOIN table2 USING (column_name); ``` | ```sql SELECT o.order_id, c.first_name, sh.name AS shipper FROM orders o JOIN customers c USING (customer_id) JOIN shippers sh USING (shipper_id); ``` |
| NATURAL JOIN | Join on columns with same name automatically | ```sql SELECT column_name(s) FROM table1 NATURAL JOIN table2; ``` | ```sql SELECT o.order_id, c.first_name FROM orders o NATURAL JOIN customers c; ``` |
| CROSS JOIN | Returns all records from both tables | ```sql SELECT column_name(s) FROM table1 CROSS JOIN table2; ``` | ```sql SELECT c.first_name AS customer, p.name AS product FROM customers c CROSS JOIN products p; ``` |
| IMPLICIT CROSS JOIN | Join tables in FROM clause separated by commas | ```sql SELECT column_name(s) FROM table1, table2; ``` | ```sql SELECT c.first_name AS customer, p.name AS product FROM customers c, products p; ``` |
| UNION | Combine result-set of two or more queries | ```sql SELECT column_name(s) FROM table1 UNION SELECT column_name(s) FROM table2; ``` | ```sql SELECT order_id, order_date, 'Active' AS status FROM orders WHERE order_date >= '2019-01-01' UNION SELECT order_id, order_date, 'Archived' AS status FROM orders WHERE order_date < '2019-01-01'; ``` |
| INSERT INTO | Insert new records | ```sql INSERT INTO table_name (column1, column2, ...) VALUES (value1, value2, ...); INSERT INTO table_name VALUES (value1, value2, ...); ``` | ```sql INSERT INTO customers VALUES (DEFAULT, 'John', 'Smith', '1990-01-01', NULL, 'address', 'city', 'CA', DEFAULT); INSERT INTO shippers (name) VALUES ('Shipper1'), ('Shipper2'), ('Shipper3'); ``` |
| CREATE TABLE | Create a new table | ```sql CREATE TABLE table_name (column1 datatype, column2 datatype, column3 datatype, ...); ``` | ```sql CREATE TABLE invoices_archived AS SELECT i.invoice_id, i.number, c.name AS client, i.invoice_total, i.payment_total, invoice_date, i.payment_date, i.due_date FROM invoices i JOIN clients c USING (client_id) WHERE i.payment_date IS NOT NULL; ``` |
| UPDATE / SET | Modify existing records | ```sql UPDATE table_name SET column1 = value1, column2 = value2, ... WHERE condition; ``` | ```sql UPDATE customers SET points = points + 50 WHERE birth_date < '1990-01-01'; ``` |
| DELETE FROM | Delete existing records | ```sql DELETE FROM table_name WHERE condition; ``` | ```sql DELETE FROM invoices WHERE client_id = (SELECT * FROM


### End of new table

### **Like Operator Patterns** {#like-operator-patterns}

| LIKE Operator | Description |
| :---- | :---- |
| WHERE CustomerName LIKE 'a%' | Finds any values that start with "a" |
| WHERE CustomerName LIKE '%a' | Finds any values that end with "a" |
| WHERE CustomerName LIKE '%or%' | Finds any values that have "or" in any position |
| WHERE CustomerName LIKE '\_r%' | Finds any values that have "r" in the second position |
| WHERE CustomerName LIKE 'a\_%' | Finds any values that start with "a" and are at least 2 characters in length |
| WHERE CustomerName LIKE 'a\_\_%' | Finds any values that start with "a" and are at least 3 characters in length |
| WHERE ContactName LIKE 'a%o' | Finds any values that start with "a" and ends with "o" |

### **Commonly Used Metacharacters in SQL REGEX** {#commonly-used-metacharacters-in-sql-regex}

| Pattern | What the Pattern matches |
| :---- | :---- |
| \* | Zero or more instances of string preceding it |
| \+ | One or more instances of strings preceding it |
| . | Any single character |
| ? | Match zero or one instances of the strings preceding it. |
| ^ | caret(^) matches Beginning of string |
| $ | End of string |
| [abc] | Any character listed between the square brackets |
| [^abc] | Any character not listed between the square brackets |
| [A-Z] | match any upper case letter. |
| [a-z] | match any lower case letter |
| [0-9] | match any digit from 0 through to 9\. |
| [[:<:]\] | matches the beginning of words. |
| [[:>:]\] | matches the end of words. |
| [:class:\] | matches a character class i.e. [:alpha:\] to match letters, [:space:\] to match white space, [:punct:\] is match punctuations and [:upper:\] for upper class letters. |
| p1\|p2\|p3 | Alternation; matches any of the patterns p1, p2, or p3 |
| {n} | Exactly n instances of preceding element |
| {m,n} | between m and n instances of preceding element |

**Commonly Used Data Types**

| Data Type | Description |
| :---- | :---- |
| CHAR(size) | A FIXED length string (can contain letters, numbers, and special characters). The size parameter specifies the column length in characters \- can be from 0 to 255\. Default is 1\.  |
| VARCHAR(size) | A VARIABLE length string (can contain letters, numbers, and special characters). The size parameter specifies the maximum column length in characters \- can be from 0 to 65535 |
| INT(size) | Signed range is from \-2147483648 to 2147483647\. Unsigned range is from 0 to 4294967295\. The size parameter specifies the maximum display width |
| DECIMAL(size, d) | An exact fixed-point number. The total number of digits is specified in size. The number of digits after the decimal point is specified in the d parameter. The maximum number for size is 65\. The maximum number for d is 30\. The default value for size is 10\. The default value for d is 0\. |
| DATE | A date. Format: YYYY-MM-DD. |
| TIME(fsp) | A time. Format: hh:mm:ss.  |
| DATETIME(fsp) | A date and time combination. Format: YYYY-MM-DD hh:mm:ss. |
| YEAR | A year in four-digit format. Values allowed in four-digit format: 1901 to 2155, and 0000\. |

