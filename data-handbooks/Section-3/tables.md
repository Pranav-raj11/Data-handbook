## Tables

### Creating Tables

* Step 1:  In your query editor, write the query (replace \*\_\* with your table and column names where required)

```sql
CREATE TABLE your_table_name (
      column_1_name column_type,
      column_2_name column_type,
      …
      column_i_name column_type,
);
```

````admonition Here’s an example:
```sql
CREATE TABLE personal_info (
        personal_id INT,
        first_name VARCHAR(50),
        last_name VARCHAR(50),
        age INT,
        gender VARCHAR(10),
        birth_date DATE
);
```
````

* Step 2: Run the code and hit the refresh button in the schemas tab. You should see your table in your database now.

```{admonition} Exercise \#2

Make a new tab. Create a table for a list of employees. Include at least 5 columns with at least 3 different data types.  
*\*For a list of data types (Int, Varchar, etc.) go to the syntax tab\**
```

### Inserting Rows Into Tables

* Step 1:  
  * In your query editor, write the query (replace \*\_\* with your table and column names where required)

```sql
INSERT INTO *your_table_name*
VALUES (*column_1_entry, column_2_entry, …, column_i_entry);
```
```` sql
```admonition Here’s an example for the table we created earlier:
INSERT INTO personal_info 
VALUES (1, ‘Michael’, ‘Scott’, 40, ‘Male’, ‘1965-03-15’),
               (2, ‘Walter', 'White', 50, 'Male', '1958-09-07'),
               (3, 'Elizabeth', 'Keen', 30, 'Female', '1985-12-20');
```
````


To view your table, in your query editor, write the query

```sql
SELECT * FROM *your_table_name*
```
```admonition For the table from earlier:
``` sql
SELECT  * FROM personal_info;
```
```


```{admonition} Exercise \#3
In the tab from exercise 2\. insert at least 5 rows to your table of employees. Use the SELECT statement to view your table.
```