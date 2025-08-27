### Writing and Running Basic Queries

#### Select Statement

To view your table, in your query editor, write the query

```sql
SELECT * FROM your_table_name
```

To view only specific columns, in your query editor, write the query

```sql
SELECT column_name_1, column_name_2, …, column_name_i FROM your_table_name
```

For the example earlier, we can show the table with only the columns name and age

``` sql
SELECT first_name, age FROM personal_info;
```

```{admonition} Exercise \#4
In the tab you used for exercise 2, try showing only three of the columns that are in your dataset.
```

#### Filtering (Where Statement)

To extract only the records that fulfill a specified condition, we use the WHERE statement with your SELECT statement 
```sql
SELECT * FROM your_table_name
WHERE condition
```

For the example earlier, we can show the table with only the columns name and age

```sql
SELECT first_name, last_name, age FROM personal_info
WHERE gender = ‘female’
```

```{tip}
There are lots of formats for writing conditions. You can use Basic comparison operators (=, \!= (or \<\>), \<, \>, \<=, \>=), multiple conditions with AND/OR: (WHERE gender \= 'Male' AND age \> 45;) and even do things like pattern matching with the LIKE operator. 

If you want to find more operators like this, check out the ‘Common Syntax’ tab for clauses like ‘In’, ‘Between’, ‘Like’ and ‘Regex’. 
```

```{admonition} Exercise \#5

In the same tab as exercise 2, create a filter using at least 1 AND/OR. 
```
#### Sorting Data (Order By Statement)

To sort the rows returned by your query, use the ORDER BY clause. You can sort results in ascending order (default) or descending order by adding DESC.

```sql
SELECT * FROM your_table_name
ORDER BY column_name (DESC if needed);
```

For the example earlier, we can order the table by age (ascending):

```sql 
SELECT first_name, last_name, age FROM personal_info
ORDER BY age;
```

Or we can order the table by age (descending):
```sql
SELECT first_name, last_name, age FROM personal_info
ORDER BY age DESC;
```

```{admonition} Exercise \#6

In the same tab as exercise 2, order your dataset by a column in descending order. 
```
#### Limiting Results (Limit Statement)

To return only a certain number of rows, use the LIMIT clause. This is helpful when working with large datasets.

```sql
SELECT * FROM your_table_name
LIMIT number_of_rows;
```

For the example earlier, we can limit to only 2 rows:

```sql 
SELECT * FROM personal_info
LIMIT 2;
```

```{admonition} Exercise \#7
In the same tab as exercise 2, use the select function while limiting results to only 3 rows. 
```

You can also stack all these clauses. 

```sql 
SELECT * FROM your_table_name
WHERE condition
ORDER BY column_name
LIMIT number_of_rows;
```

```{admonition} Exercise \#8

In the same tab as exercise 2, show your dataset while using all of the SELECT, WHERE, ORDER BY and LIMIT clauses. Now save this script with exercises 2-7 into your folder. 
```