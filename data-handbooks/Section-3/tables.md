## Tables

### Creating Tables

* Step 1:  In your query editor, write the query (replace \*\_\* with your table and column names where required)

| CREATE TABLE \*your\_table\_name\* (       \*column\_1\_name\* \*column\_type\*,       \*column\_2\_name\* \*column\_type\*,       …       \*column\_i\_name\* \*column\_type\*, ); |
| :---- |

  * Here’s an example:

| CREATE TABLE personal\_info (         personal\_id INT,         first\_name VARCHAR(50),         last\_name VARCHAR(50),         age INT,         gender VARCHAR(10),         birth\_date DATE ); |
| :---- |

    

* Step 2: Run the code and hit the refresh button in the schemas tab. You should see your table in your database now.

### Exercise \#2

Make a new tab. Create a table for a list of employees. Include at least 5 columns with at least 3 different data types.  
*\*For a list of data types (Int, Varchar, etc.) go to the syntax tab\**

### Inserting Rows Into Tables

* Step 1:  
  * In your query editor, write the query (replace \*\_\* with your table and column names where required)

| INSERT INTO \*your\_table\_name\* VALUES (\*column\_1\_entry, column\_2\_entry, …, column\_i\_entry); |
| :---- |

  * Here’s an example for the table we created earlier:

| INSERT INTO personal\_info  VALUES (1, ‘Michael’, ‘Scott’, 40, ‘Male’, ‘1965-03-15’),                (2, ‘Walter', 'White', 50, 'Male', '1958-09-07'),                (3, 'Elizabeth', 'Keen', 30, 'Female', '1985-12-20'); |
| :---- |

To view your table, in your query editor, write the query

| SELECT \* FROM \*your\_table\_name\* |
| :---- |

* For the table I created earlier:

| SELECT  \* FROM personal\_info; |
| :---- |

### Exercise \#3

In the tab from exercise 2\. insert at least 5 rows to your table of employees. Use the SELECT statement to view your table.