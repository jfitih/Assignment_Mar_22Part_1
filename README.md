# Assignment_Mar_22Part_1
sql code
PART – I 
 
Note: The keywords written in uppercase are SQL keywords. 
 
 
Problem 01: Retrieving Records: you have a table and want to see all of the data. 
 
SELECT  *  FROM table_name 
 
Discussion: ‘*’ will return every column of the table. Note that columns are typically the attributes of the entity (row). 
 
Problem 02: View only selective columns of the table. 
 
SELECT age, sex, salary 
FROM table_name 
 
Discussion: Here, age, sex, salary are the names of columns of the table.  
 
Problem 03: View only selective rows that satisfy certain conditions. For example, show the name, age, and salary of employees whose age is greater than 35 years. 
 
SELECT name, age, salary            FROM table_name WHERE age>35 
 
Note: Conditional operators such as =, <, >, <=, >=, !, <> are supported in SQL. 
 
Problem 04: Display rows that satisfy multiple conditions. Following the WHERE clause use the OR and AND statements. Show the employees who earn less than $2000 and are over 40 years of age or who are females. 
 
SELECT *       FROM table_name WHERE (salary<2000 AND age>40)               OR sex = Female 
 
 
Problem 05: Rename the columns and then view the table with the newly named column. Here, sal and dept are the original column names in the table.  
 
SELECT sal AS Salary, dept AS Department     FROM table_name 
 
Problem 06: Concatenating column values to combine multiple columns into one. 
 
SELECT concat(first_name, last_name) AS names   FROM table_name WHERE Salary>2000 
 
Problem 07: Implement IF-ELSE statement: for example: if the customer pays less than $100, more than $100, and equal to $100, mark him as underpaid, overpaid, and paid, respectively.  
 
SELECT names, salary, CASE WHEN salary <= 100 then ‘UNDERPAID’   WHEN salary >= 4000 then ‘OVERPAID’ ELSE ‘PAID’  END AS paymentStatus FROM table_name 
 

 Problem 08: Limit the number of rows – show only top n rows of the table. Note that row represents the entity/item/individual sample and columns represent the attributes. The SQL statements are often different across different database platforms as you can see in the table below. 
 
 
 
 
 DB2 MySQL, PostgreSQL Oracle SQL Server Select first five rows SELECT * FROM table_name FETCH FIRST 5 rows only SELECT *  FROM table_name LIMIT 5 
 SELECT *  FROM table_name WHERE ROWNUM <=5 
 SELECT top 5* FROM table_name 
 
 
Problem 09: Returning n random records from a table 
 
SELECT name, age FROM table_name ORDER BY rand() limit 5 
 
Note ORDER BY clause can accept a function’s return value and use it to change the order of the result set. Here, the rand() function is performed first to get the random rows and then it is ordered to show the first 5 rows in the randomly arranged rows. 
 
Problem 10: Find all the rows that have NULL or missing entries in a particular column 
 
SELECT * FROM table_name WHERE column_name IS NULL Note you can use IS NOT NULL to select columns free of NULL entries. 
 
Problem 10: Transforming NULL entries into REAL values. Use COALESCE function to substitute real values for NULL 
 
SELECT COALESCE (col_name, 0) FROM table_name 
 
Replaces all the null entries in column col_name by 0. Alternatively, you can use CASE (IF-ELSE equivalent in SQL) as below 
 
SELECT CASE  WHEN col_name is NULL THEN 0 ELSE col_name  
END From table_name 
 
Problem 11: Search rows with specific patterns in a particular column. Below is an example of selecting student name and age from the table belonging to 5th and 8th grade. 
 
SELECT name, age FROM table_name WHERE grade_num IN (5, 8) 
 
Problem 11: Use of wildcard operator % to search rows that have specific substring pattern. 
 
SELECT name, age FROM table_name WHERE grade_num (5, 8) AND (name LIKE ‘%th%’ or name LIKE ‘%son’) 
 
The example above identifies the rows or students who belong to either 5th or 8th grade and have “th” string in anywhere of their name string – use % on both sides. If you are looking for the substring ‘son’ at the end of the name (Davidson) use % followed by the substring.

USE employees;
-- PART – I 
 
-- Note: The keywords written in uppercase are SQL keywords. 
 
 
-- Problem 01: Retrieving Records: you have a table and want to see all of the data. 
 
SELECT  *  FROM table_name; 

SELECT  *  FROM departments; 
SELECT  *  FROM dept_emp;
SELECT  *  FROM dept_manager;
SELECT  *  FROM employees;
SELECT  *  FROM salaries;
SELECT  *  FROM titles;
 
-- Discussion: ‘*’ will return every column of the table. 
-- Note that columns are typically the attributes of the entity (row). 
 
-- Problem 02: View only selective columns of the table. 
 
SELECT age, sex, salary 
FROM table_name; 
 
SELECT birth_date, gender, salary 
FROM employees join salaries; 

-- Discussion: Here, age, sex, salary are the names of columns of the table.  
 
-- Problem 03: View only selective rows that satisfy certain conditions. 
-- For example, show the name, age, and salary of employees whose age is 
-- greater than 35 years. 

SELECT name, age, salary            
FROM table_name WHERE age>35; 
 
 
SELECT concat(first_name, '  ', last_name) AS names, gender, salary            
FROM employees join salaries WHERE birth_date>35; 


 
-- Note: Conditional operators such as =, <, >, <=, >=, !, <> are supported in SQL. 

/* 
 Problem 04: Display rows that satisfy multiple conditions. 
Following the WHERE clause use the OR and AND statements. 
Show the employees who earn less than $2000 and are over 
40 years of age or who are females. 
 */
 
 
SELECT *       
FROM table_name 
WHERE (salary<2000 AND age>40)               
OR sex = Female; 

SELECT *       
FROM employees,salaries 
WHERE (salary<2000 AND birth_date>40)               
OR gender = 'F'; 
 
/* 
Problem 05: Rename the columns and then view 
the table with the newly named column. 
Here, sal and dept are the original 
column names in the table.  
 */
 
 
SELECT sal AS Salary, dept AS Department     FROM table_name; 

SELECT salary AS Salary, dept_name AS Department     FROM employees,salaries,departments; 
 
-- Problem 06: Concatenating column values to combine multiple columns into one. 
 
SELECT concat(first_name, last_name) AS names   FROM table_name WHERE Salary>2000;

SELECT concat(first_name,'  ', last_name) AS names , salary, gender  
FROM employees, salaries 
WHERE (Salary>2000);
-- ORDER BY last_name DESC; 
 
SELECT concat(first_name,'  ', last_name) AS names , salary, gender  
FROM employees, salaries 
WHERE (Salary>2000)
ORDER BY last_name DESC; 


/*
 Problem 07: Implement IF-ELSE statement: 
for example: if the customer pays less than $100, 
more than $100, and equal to $100, mark him as 
underpaid, overpaid, and paid, respectively.  
*/

SELECT names, salary, 
CASE 
WHEN salary <= 100 then ‘UNDERPAID’   
WHEN salary >= 4000 then ‘OVERPAID’ 
ELSE ‘PAID’  
END AS paymentStatus 
FROM table_name; 
 
SELECT concat(first_name,'  ', last_name) AS names, salary, CASE WHEN salary <= 100 then 'UNDERPAID'   WHEN salary >= 4000 then 'OVERPAID' ELSE 'PAID'  END AS paymentStatus FROM table_name; 
 

SELECT concat(first_name,'  ', last_name) AS names, salary, title, 
CASE 
WHEN salary <= 100 then 'UNDERPAID'   
WHEN salary >= 4000 then 'OVERPAID' 
ELSE 'PAID'  
END AS paymentStatus 
FROM employees, salaries, titles; 

 -- Problem 08: Limit the number of rows – show only top n rows of the table. Note that row represents the entity/item/individual sample and columns represent the attributes. The SQL statements are often different across different database platforms as you can see in the table below. 
 
 
 
 
-- DB2 | MySQL, PostgreSQL | Oracle | SQL Server 
-- Select first five rows 

-- SELECT * FROM table_name FETCH FIRST 5 rows only;  # DB2 
SELECT *  FROM table_name LIMIT 5;                 # MySQL, PostgreSQL
SELECT *  FROM table_name WHERE ROWNUM <=5;        # Oracle
-- SELECT top 5* FROM table_name;                     # SQL Server 

SELECT *  
FROM table_name LIMIT 5;                 # MySQL, PostgreSQL
SELECT *  
FROM table_name WHERE ROWNUM <=5;        # Oracle 
 
 
SELECT *  
FROM departments LIMIT 5;                 # MySQL, PostgreSQL
SELECT *  
FROM departments WHERE dept_name <= 11;        # Oracle 

SELECT *  
FROM dept_emp LIMIT 1500;                 # MySQL, PostgreSQL
SELECT *  
FROM dept_emp WHERE dept_no <=5;        # Oracle 
SELECT *  
FROM dept_emp, employees where gender = 'f'
LIMIT 1500;                 # MySQL, PostgreSQL

SELECT *  
FROM dept_manager LIMIT 5;                 # MySQL, PostgreSQL
SELECT *  
FROM dept_manager WHERE dept_no <=5;        # Oracle 

SELECT *  
FROM employees LIMIT 5;                 # MySQL, PostgreSQL
SELECT *  
FROM employees WHERE hire_date <=5;        # Oracle 

SELECT *  
FROM salaries LIMIT 5;                 # MySQL, PostgreSQL
SELECT *  
FROM salaries WHERE salary <=5;        # Oracle  

SELECT *  
FROM titles, salaries LIMIT 5;                 # MySQL, PostgreSQL
SELECT *  
FROM titles, salaries WHERE title = 'Engineer';        # Oracle  



-- Problem 09: Returning n random records from a table 
 
SELECT name, age FROM table_name ORDER BY rand() limit 5; 
 
SELECT concat(first_name,'  ', last_name) AS names, birth_date 
FROM employees ORDER BY rand() limit 5; 
 
 
-- Note ORDER BY clause can accept a function’s return value and use it to change the order of the result set. Here, the rand() function is performed first to get the random rows and then it is ordered to show the first 5 rows in the randomly arranged rows. 
 
-- Problem 10: Find all the rows that have NULL or missing entries in a particular column 
 
SELECT * FROM table_name WHERE column_name IS NULL ;

SELECT * 
FROM employees join salaries
WHERE birth_date IS NULL;

SELECT * 
FROM employees 
WHERE birth_date IS NOT NULL;

SELECT * 
FROM salaries 
WHERE salary IS NOT NULL;

-- Note you can use IS NOT NULL to select columns free of NULL entries. 
 
-- Problem 10: Transforming NULL entries into REAL values. Use COALESCE function to substitute real values for NULL 
 
SELECT COALESCE (col_name, 0) FROM table_name; 

SELECT * , COALESCE (salary, 0) FROM salaries; 
 
SELECT COALESCE (emp_no, 0) FROM salaries;
SELECT COALESCE (title, 0) FROM titles;

/*
 Replaces all the null entries in column col_name by 0. 
Alternatively, you can use CASE (IF-ELSE equivalent in SQL) as below 
*/ 

SELECT CASE  WHEN col_name is NULL THEN 0 ELSE col_name  
END From table_name; 

SELECT *,
CASE  
WHEN salary is NULL THEN 0 ELSE emp_no  
END From salaries; 
 
-- 
/*Problem 11: Search rows with specific patterns in a particular column. 
Below is an example of selecting student name and age 
from the table belonging to 5th and 8th grade. 
*/

 
SELECT name, age 
FROM table_name 
WHERE grade_num IN (5, 8); 

SELECT concat(first_name,'  ', last_name) AS names, birth_date, gender, salary, title 
FROM employees, salaries, titles 
WHERE title IN ('Senior','Engineering');
 
/*-- 
Problem 11: Use of wildcard operator % to search rows 
that have specific substring pattern. 
 */
 
SELECT name, age 
FROM table_name 
WHERE grade_num (5, 8) 
AND (name LIKE ‘%th%’ or name LIKE ‘%son’); 
 
SELECT concat(first_name,'  ', last_name) AS names, birth_date 
FROM  titles join employees
WHERE title ('Senior','Engineering') 
AND (name LIKE '%th%' or name LIKE '%so'); 
 
/*The example above identifies the rows or 
students who belong to either 5th or 8th grade 
and have “th” string in anywhere of their name 
string – use % on both sides. If you are looking 
for the substring ‘son’ at the end of the name 
(Davidson) use % followed by the substring. 
*/

PART – II 
  Sorting Query Results 
 
Problem 01: Sort the rows based on ascending order of the salary (from lowest to highest) 
 
 
SELECT names, salary, age FROM table_name WHERE age>25 ORDER BY salary asc 
 
Default is ascending order: ORDER BY salary For descending order: ORDER BY salary desc 
 
Note that you need to specify the column name based on which the ordering will be done. Instead, you can use the column number after ORDER BY. 
 
Problem 02: Sort the rows based on multiple fields or columns. For example, sort the table first based on ascending order of the age and then descending order of the salary. 
 
SELECT names, salary 
FROM table_name ORDER BY age, salary desc 
 
Warning: You can ORDER BY a column without displaying or selecting the column – see age was not next to SELECT. However, when using GROUP BY or DISTINCT, you cannot ORDER BY columns without having it next to SELECT.  
 
Problem 03: Sort the rows based on the alphabetic order of substring in a column. 
 
SELECT name, age, salary FROM table_name ORDERBY SUBSTR (name, length(name) – 2) 
 
Here SUBSTR (column_name, start_index of the string). Where, length(name) – 2 → last two characters of a string.  
 
Problem 04: Order NULL entries of the salary field in descending order and non-null in ascending order. We create a new field called is_null that contains the flag related to the NULL status – we use CASE to implement IF-ELSE condition on the salary column  
 
 
 
 
SELECT name, age, salary FROM ( SELECT name, age, salary,  CASE WHEN salary IS NULL THEN 0 ELSE 1 END AS is_null FROM table_name ) x ORDER BY is_null desc, salary ) 
 
Quiz: How do you place or push all NULL entries at the end 
 
Problem 05: Sort rows based on a conditional logic. When Sex = Female, create a separate column to display their salary in ascending order.  
 
SELECT name, age, sex, salary, new_col,  CASE WHEN sex = ‘FEMALE’ then new_col  else salary end as ordered FROM table_name ORDER BY ORDERED 
 
 
Problem 06: Find the age in years at the time of hire use the date of hire and the birth date of male employees only. 
 
SELECT first_name, last_name, DATEDIFF(hire_date, birth_date)/365 AS age_hire  FROM  employees WHERE gender = 'M' ; 
 
 
Problem 07: You cannot use field aliases in the WHERE clause as below. 
 
INCORRECT 
 
SELECT first_name, DATEDIFF(hire_date, birth_date)/365 AS age_hire  FROM  employees WHERE age_hire>28; 
 
CORRECT  
 
SELECT first_name, DATEDIFF(hire_date, birth_date)/365 AS  age_hire  FROM  employees WHERE (DATEDIFF(hire_date, birth_date)/365)>28; 
 
OR: You can create an internal table to make this happen as below 
 
 
SELECT    * FROM (  SELECT      first_name, DATEDIFF(hire_date, birth_date)/365 AS daysdiff    FROM employees ) as INNERTABLE WHERE daysdiff >28

