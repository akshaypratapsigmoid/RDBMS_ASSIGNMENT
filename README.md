# RDBMS_Assignment
Repository for RDBMS assignment

### 1. Create a database named employee, then import data_science_team.csv proj_table.csv and emp_record_table.csv into the employee database from the given resources.    
### Query:   

create database employee;  
use employee;  

●  As asked I have imported data_science_team.csv, proj_table.csv and emp_record_table.csv into the employee database from the given resources using MySQLWorkbench.  

### 2. Create an ER diagram for the given employee database.    
### ER Diagram:  

![image (1)](https://user-images.githubusercontent.com/122514456/220896901-7f82ce85-7f7f-4916-9a06-5169e01c0a4f.png)

   							
### 3. Write a query to fetch EMP_ID, FIRST_NAME, LAST_NAME, GENDER, and DEPARTMENT from the employee record table, and make a list of employees and details of their department.   
### Query:    

SELECT emp_id, first_name, last_name, gender, dept  
FROM emp_record_table;

### Output:  
<img width="1226" alt="Screenshot 2023-02-23 at 4 27 03 PM" src="https://user-images.githubusercontent.com/122514456/220887917-6f5eca30-86f0-4606-ae71-1c0c5c712df4.png">


### 4. Write a query to fetch EMP_ID, FIRST_NAME, LAST_NAME, GENDER, DEPARTMENT, and EMP_RATING if the EMP_RATING is:	
●  less than two  
●  greater than four  
● between two and four   
### Query:  

### 4a:  
SELECT emp_id, first_name, last_name, gender, dept, emp_rating  
FROM emp_record_table  
WHERE emp_rating<2;  

### Output:  
<img width="1226" alt="Screenshot 2023-02-23 at 4 28 18 PM" src="https://user-images.githubusercontent.com/122514456/220887952-d904db88-e499-413f-bfdf-369ede7dc561.png">


### 4b:  
SELECT emp_id, first_name, last_name, gender, dept, emp_rating   
FROM emp_record_table  
WHERE emp_rating>4;  

### Output:  
<img width="1226" alt="Screenshot 2023-02-23 at 4 29 56 PM" src="https://user-images.githubusercontent.com/122514456/220888130-f638b343-e535-4859-8a69-f9cc1dcb4d4f.png">


### 4c:  
SELECT emp_id, first_name, last_name, gender, dept, emp_rating  
FROM emp_record_table  
WHERE emp_rating BETWEEN 2 AND 4;  

### Output:  
<img width="1226" alt="Screenshot 2023-02-23 at 4 36 15 PM" src="https://user-images.githubusercontent.com/122514456/220889331-29ffbf87-f281-44a8-a4f4-e2cbcc64e73c.png">


### 5. Write a query to concatenate the FIRST_NAME and the LAST_NAME of employees in the Finance department from the employee table and then give the resultant column alias as NAME.  
### Query:  

SELECT CONCAT(first_name, ' ', last_name) as NAME  
FROM emp_record_table  
WHERE dept='Finance';  

### Output:  
<img width="1225" alt="Screenshot 2023-02-23 at 3 59 58 PM" src="https://user-images.githubusercontent.com/122514456/220882022-d38c61a9-4da6-49c7-aa31-c798a47fdb59.png">


### 6. Write a query to list only those employees who have someone reporting to them. Also, show the number of reporters (including the President). 
### Query:   

SELECT mgr.emp_id, mgr.first_name, mgr.last_name, COUNT(e.emp_id)  
FROM emp_record_table AS e INNER JOIN emp_record_table AS mgr   
ON e.manager_id = mgr.emp_id  
GROUP BY mgr.emp_id, mgr.first_name, mgr.last_name;  

### Output:  
<img width="1225" alt="Screenshot 2023-02-23 at 4 01 10 PM" src="https://user-images.githubusercontent.com/122514456/220882234-1f4cb5a8-db85-4d83-8c1c-f0c080a0c628.png">


### 7. Write a query to list down all the employees from the healthcare and finance departments using union. Take data from the employee record table. 
### Query:   

SELECT emp_id, first_name, last_name, dept  
FROM emp_record_table  
WHERE dept='Healthcare'  
UNION  
SELECT emp_id, first_name, last_name, dept   
FROM emp_record_table  
WHERE dept='Finance';  

### Output:  
<img width="1226" alt="Screenshot 2023-02-23 at 4 02 46 PM" src="https://user-images.githubusercontent.com/122514456/220882553-e42d1fc1-b14e-4bb7-8da5-89ef3bd4f3ff.png">


### 8. Write a query to list down employee details such as EMP_ID, FIRST_NAME, LAST_NAME, ROLE, DEPARTMENT, and EMP_RATING grouped by dept. Also include the respective employee rating along with the max emp rating for the department. 
### Query:  

SELECT emp_id, first_name, last_name, role, dept, emp_rating,  
max(emp_rating) OVER(PARTITION BY dept) as max_rating_by_dept  
FROM emp_record_table;  

### Output:  
<img width="1226" alt="Screenshot 2023-02-23 at 4 23 24 PM" src="https://user-images.githubusercontent.com/122514456/220887181-c000ad04-3982-4978-845a-85729f3202e1.png">


### 9. Write a query to calculate the minimum and the maximum salary of the employees in each role. Take data from the employee record table.   	
### Query:  

SELECT MIN(salary) as min_sal_by_role, MAX(salary) as max_sal_by_role  
FROM emp_record_table  
GROUP BY role;  

### Output:  
<img width="1228" alt="Screenshot 2023-02-23 at 4 04 58 PM" src="https://user-images.githubusercontent.com/122514456/220883009-bf1e6cf7-a019-4d44-8d37-3686166bdbe2.png">


### 10. Write a query to assign ranks to each employee based on their experience. Take data from the employee record table.   
### Query:    

SELECT DISTINCT emp_id, exp, DENSE_RANK() OVER(ORDER BY exp DESC) AS rank_by_exp   
FROM emp_record_table;   

### Output:  
<img width="1227" alt="Screenshot 2023-02-23 at 4 06 06 PM" src="https://user-images.githubusercontent.com/122514456/220883261-041d97d5-9993-462a-aad1-489134db028a.png">


### 11. Write a query to create a view that displays employees in various countries whose salary is more than six thousand. Take data from the employee record table.   			
### Query:  

CREATE OR REPLACE VIEW sal_greater_six_K    
AS SELECT emp_id, first_name, last_name, country, salary   
FROM emp_record_table    
WHERE salary>6000;    

SELECT * FROM sal_greater_six_K;

### Output:  
<img width="1227" alt="Screenshot 2023-02-23 at 4 07 29 PM" src="https://user-images.githubusercontent.com/122514456/220883550-40d520f3-171f-40c0-a80b-41344faee5ae.png">

			
### 12. Write a nested query to find employees with experience of more than ten years. Take data from the employee record table.   			
### Query:  

SELECT *   
FROM emp_record_table    
WHERE emp_id IN  
(SELECT emp_id   
FROM emp_record_table  
WHERE exp>10);  

### Output:  
<img width="1227" alt="Screenshot 2023-02-23 at 4 09 59 PM" src="https://user-images.githubusercontent.com/122514456/220884001-561f709a-1138-44e8-b39d-c2b701522057.png">


### 13. Write a query to create a stored procedure to retrieve the details of the employees whose experience is more than three years. Take data from the employee record table.   	
### Query:  

delimiter $$  
create procedure emp_details()  
begin  
	select * from emp_record_table  
    	where exp>3;  
end$$  
delimiter ;  
call emp_details();  

### Output:  
<img width="1227" alt="Screenshot 2023-02-23 at 4 11 11 PM" src="https://user-images.githubusercontent.com/122514456/220884263-61af9d41-b80b-44eb-8497-1d3cf6635541.png">

	
### 14. Write a query using stored functions in the project table to check whether the job profile assigned to each employee in the data science team matches the organization’s set standard.  
### The standard being:		   
### For an employee with experience less than or equal to 2 years assign 'JUNIOR DATA SCIENTIST', For an employee with the experience of 2 to 5 years assign 'ASSOCIATE DATA SCIENTIST',  
### For an employee with the experience of 5 to 10 years assign 'SENIOR DATA SCIENTIST',  
### For an employee with the experience of 10 to 12 years assign 'LEAD DATA SCIENTIST',		  			
### For an employee with the experience of 12 to 16 years assign 'MANAGER'.   
### Query:  

delimiter $$  
create function emp_details() returns tinyint(1) deterministic  
begin  
	declare v_exp int default 0;  
	declare v_role varchar(50) default "";  
    	declare finished int default 0;  
	declare dummy_cursor cursor for  
		select exp, role from emp_record_table;   
	declare continue handler for not found   
		set finished=1;   
	open dummy_cursor;   
	check_role: loop   
		fetch dummy_cursor into v_exp, v_role;   
       		if finished = 1 then   
         		leave check_role;   
		end if;   
        	if (v_exp<=2 and v_role!='JUNIOR DATA SCIENTIST') then   
			return false;  
		elseif (v_exp>2 and v_exp<=5 and v_role!='ASSOCIATE DATA SCIENTIST') then  
			return false;  
       		elseif (v_exp>5 and v_exp<=10 and v_role!='SENIOR DATA SCIENTIST') then  
			return false;  
        	elseif (v_exp>10 and v_exp<=12 and v_role!='LEAD DATA SCIENTIST') then  
 			return false;  
       		elseif (v_exp>12 and v_exp<=16 and v_role!='MANAGER') then  
			return false;  
       		end if;  
        
    end loop check_role;  
    close dummy_cursor;  
    return true;  
end$$  
delimiter ;  

delimiter $$  
create procedure helper_procedure()  
begin  
	if emp_details() then  
 		select 'The job profile assigned to each employee  
in the data science team matches the organization’s set standard.' as message;  
	else  
		select 'The job profile assigned to each employee   
in the data science team does not match the organization’s set standard.' as message;  
	end if;  
end$$  
delimiter ;  
call helper_procedure();  

### Output:  
<img width="1225" alt="Screenshot 2023-02-23 at 4 13 14 PM" src="https://user-images.githubusercontent.com/122514456/220884715-9685f360-f80d-497d-9ab8-20701a964946.png">


### 15. Create an index to improve the cost and performance of the query to find the employee whose FIRST_NAME is ‘Eric’ in the employee table after checking the execution plan.   
### Query:  

create index ename_index  
on emp_record_table(first_name);  
select *  
from emp_record_table  
where first_name = 'Eric';  

### Output:  
<img width="1226" alt="Screenshot 2023-02-23 at 4 17 35 PM" src="https://user-images.githubusercontent.com/122514456/220885607-1f7c6b0e-d9d7-494e-8868-fbb3faed2966.png">


### 16. Write a query to calculate the bonus for all the employees, based on their ratings and salaries (Use the formula: 5% of salary * employee rating). 
### Query:

select emp_id, emp_rating, salary, (0.05\*salary\*emp_rating) as bonus    
from emp_record_table;   

### Output:  
<img width="1225" alt="Screenshot 2023-02-23 at 4 19 37 PM" src="https://user-images.githubusercontent.com/122514456/220886031-a022f5d7-844d-4601-92d4-0e4a7ce2f0de.png">


### 17. Write a query to calculate the average salary distribution based on the continent and country. Take data from the employee record table.   
### Query:   

select distinct continent, avg(salary) over(partition by continent) as avg_sal_by_continent,  
country, avg(salary) over(partition by country) as avg_sal_by_country  
from emp_record_table;  

### Output:  
<img width="1225" alt="Screenshot 2023-02-23 at 4 20 41 PM" src="https://user-images.githubusercontent.com/122514456/220886237-e97501b5-0435-4876-ae5e-0569ece75c18.png">
