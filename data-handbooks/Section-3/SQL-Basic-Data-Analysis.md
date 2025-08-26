## **Section 3: Basic Data Analysis**

### Navigating MySQL Workbench

MySQL Workbench is MySQL’s official graphical interface for working with databases. It lets you do things like: 

* Connect to and manage MySQL servers  
* write/execute SQL queries  
* Explore data visually  
* export/import data easily

**Step 1:** Open MySQL Workbench  
**Step 2:** You should see ‘Local instance’ under MySQL Connections. If you **don’t**, follow these steps: 

* Click the plus beside *MySQL Connections*  
* Give the connection a name like ‘Local Instance’  
* Click on *Store in Keychain …* or *Store in Vault …* to enter the password made during installation  
* Test the connection and click *OK*

Every time you open MySQL Workbench, use this connection to connect to your local server. 

![][image1] 
 
*\*This is MySQL Workbench on macOS. Windows will look slightly different but overall, they’re almost identical in terms of functionality\**

1. Create a new tab for writing SQL code (queries)  
2. Opening a SQL file  
3. Administration tab: used to do administrative work like starting/stopping a server, importing/exporting schemas and more  
4. Schemas tab: shows the databases that we have in the current database server. Right now, we just have sys (the database that MySQL uses internally to do its work) and maybe Sakila if you’re on Windows  
5. Run’s the query  
6. Query Editor Window: where we right SQL code  
7. Output panel/results grid \- where your query results/tables will appear

I will refer to some of these later on with a number in brackets (eg. (2))

### Databases

You can think of a database as a folder. It acts as a container. Tables would be the files within the database (folder).   
**Creating a Database:**

* Step 1: In your query editor, write the query (replace \*\_\* with your db name)

| CREATE DATABASE \*your\_database\_name\*; |
| :---- |

- When you make MySQL queries, there is no case sensitivity so you don’t need to worry about capitalization of anything. A good format to follow, however, is using uppercase for keywords like CREATE DATABASE or SELECT (clause that you will learn soon)  
* Step 2: Click on the lightning bolt button (\#5 in the legend from earlier) to execute the statement  
  * You will see in your output (7) that the action was successful (green check)  
* Step 3: Select the Schemas tab (4) and hit the refresh button beside where it says schemas. You should now see your new database. 

![][image2]

**Use the database:** 

There are two ways: 

Method 1: Right click on the database and click on ‘Set as Default Schema’  
![][image3]  
Method 2: In your query editor, write the query (replace \*\_\* with your db name)

| USE \*your\_database\_name\*; |
| :---- |

**Drop the database:**

* Step 1: In your query editor, write the query (replace \*\_\* with your db name)

| DROP DATABASE \*your\_database\_name\*; |
| :---- |

* Step 2: Click on the lightning bolt button (\#5 in the legend from earlier) to execute the statement  
  * You will see in your output (7) that the action was successful (green check)  
* Step 3: Select the Schemas tab (4) and hit the refresh button beside where it says schemas. You should not see your database now.

### Saving Queries

To save your query, click on the save icon in the tool bar (near lightning bolt) \-\> ![][image4]  
Alternatively, you could click on file → save script as  
To create a new query tab, click on the new file icon (1) on the top left ![][image5]

Important Notes About Running Queries

* End each SQL statement with a semicolon (;). This tells SQL that the current statement is complete.  
* When you run a script, MySQL Workbench only executes the statement your cursor is currently inside (or the text you have highlighted).  
* If your cursor is on the second line, only that statement will run, not the entire file.  
* To run all queries in the file, highlight them all first, then click the Execute button (⚡).  
* For this project, you can do all the learning queries in 1 tab if you’d like, however, do the exercises in separate tabs. 

### Exercise \#1

Make a new tab. Create a database and use it. Save this script into a folder for the work you’ll do in this handbook. 

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

### Writing and Running Basic Queries

#### Select Statement

To view your table, in your query editor, write the query

| SELECT \* FROM \*your\_table\_name\* |
| :---- |

To view only specific columns, in your query editor, write the query

| SELECT column\_name\_1, column\_name\_2, …, column\_name\_i FROM \*your\_table\_name\* |
| :---- |

For the example earlier, we can show the table with only the columns name and age

| SELECT first\_name, age FROM personal\_info; |
| :---- |

### Exercise \#4

In the tab you used for exercise 2, try showing only three of the columns that are in your dataset.

#### Filtering (Where Statement)

To extract only the records that fulfill a specified condition, we use the WHERE statement with your SELECT statement 

| SELECT \* FROM \*your\_table\_name\* WHERE *condition* |
| :---- |

For the example earlier, we can show the table with only the columns name and age

| SELECT first\_name, last\_name, age FROM personal\_info WHERE gender \= ‘female’ |
| :---- |

There are lots of formats for writing conditions. You can use Basic comparison operators (=, \!= (or \<\>), \<, \>, \<=, \>=), Multiple conditions with AND/OR: (WHERE gender \= 'Male' AND age \> 45;) and even do things like pattern matching with the LIKE operator. If you want to find more operators like this, check out the ‘Common Syntax’ tab for clauses like ‘In’, ‘Between’, ‘Like’ and ‘Regex’. 

### Exercise \#5

In the same tab as exercise 2, create a filter using at least 1 AND/OR. 

#### Sorting Data (Order By Statement)

To sort the rows returned by your query, use the ORDER BY clause. You can sort results in ascending order (default) or descending order by adding DESC.

| SELECT \* FROM \**your\_table\_name*\* ORDER BY *column\_name* (DESC *if needed)*; |
| :---- |

For the example earlier, we can order the table by age (ascending):

| SELECT first\_name, last\_name, age FROM personal\_info ORDER BY age; |
| :---- |

Or we can order the table by age (descending):

| SELECT first\_name, last\_name, age FROM personal\_info ORDER BY age DESC; |
| :---- |

### Exercise \#6

In the same tab as exercise 2, order your dataset by a column in descending order. 

#### Limiting Results (Limit Statement)

To return only a certain number of rows, use the LIMIT clause. This is helpful when working with large datasets.

| SELECT \* FROM \**your\_table\_name*\* LIMIT *number\_of\_rows*; |
| :---- |

For the example earlier, we can limit to only 2 rows:

| SELECT \* FROM personal\_info LIMIT 2; |
| :---- |

### Exercise \#7

In the same tab as exercise 2, use the select function while limiting results to only 3 rows. 

You can also stack all these clauses. 

| SELECT \* FROM \**your\_table\_name*\* WHERE *condition* ORDER BY *column\_name* LIMIT *number\_of\_rows*; |
| :---- |

### Exercise \#8

In the same tab as exercise 2, show your dataset while using all of the SELECT, WHERE, ORDER BY and LIMIT clauses. Now save this script with exercises 2-7 into your folder. 
