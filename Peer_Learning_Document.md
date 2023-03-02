## RDBMS Peer Learning Document

### Karan's Way


## Solution 1:

CREATE DATABASE employee; 
USE employee;

* After creating the database I Imported the given csv files through GUI of the
  MYSQL Workbench.


## Solution 2:

![MergedImages (2)](https://user-images.githubusercontent.com/122456892/220898377-f57bdd5c-6fa1-4927-a656-a3433e4c3e3d.png)


## Solution 3:

* _Fetching the required data columns from emp_record_table_

SELECT ert.EMP_ID, ert.FIRST_NAME, ert.LAST_NAME, ert.GENDER, ert.DEPT
FROM emp_record_table ert;


* _Considering ert as an alias for emp_record_table_

### OUTPUT:
<img width="634" alt="Screenshot 2023-02-23 at 2 23 42 PM" src="https://user-images.githubusercontent.com/122456892/220861022-8c94bef9-8ac1-406b-8e21-848102c66b14.png">

## Solution 4:

* Query to fetch required data columns where employee rating(EMP_RATING) is
   LESS THAN 2

SELECT ert.EMP_ID, ert.FIRST_NAME, ert.LAST_NAME, ert.GENDER, ert.DEPT , ert.EMP_RATING
FROM emp_record_table ert
WHERE ert.EMP_RATING < 2;


### OUTPUT:
<img width="626" alt="Screenshot 2023-02-23 at 2 32 06 PM" src="https://user-images.githubusercontent.com/122456892/220862776-62d48a7e-c02d-4bf2-b0fd-1d58a5a8ede6.png">

* Query to fetch required data columns where employee rating(EMP_RATING) is
  GREATER THAN 4
 
 
SELECT ert.EMP_ID, ert.FIRST_NAME, ert.LAST_NAME, ert.GENDER, ert.DEPT, ert.EMP_RATING
FROM emp_record_table ert
WHERE ert.EMP_RATING > 4;
 
 
 ### OUTPUT:
 <img width="626" alt="Screenshot 2023-02-23 at 2 33 01 PM" src="https://user-images.githubusercontent.com/122456892/220862935-aa4708de-b4aa-4a44-a53a-8178fd253651.png">

  
* Query to fetch required data columns where employee rating(EMP_RATING) is
  BETWEEN 2 AND 4
  

SELECT ert.EMP_ID, ert.FIRST_NAME, ert.LAST_NAME, ert.GENDER, ert.DEPT , ert.EMP_RATING
FROM emp_record_table ert
WHERE ert.EMP_RATING between 2 and 4;


### OUTPUT:
<img width="626" alt="Screenshot 2023-02-23 at 2 34 43 PM" src="https://user-images.githubusercontent.com/122456892/220863293-a9edf275-5cf3-4281-b764-2db74dfe1b4d.png">


## Solution 5:

SELECT CONCAT(ert.FIRST_NAME,' ',ert.LAST_NAME) as NAME 
FROM emp_record_table ert                                
where ert.dept='FINANCE';

_Approach:-_

* _Concatenating_ First_name and last name of employees with alias as _NAME_ from emp_record_table where department is _FINANCE_

### OUTPUT:
<img width="626" alt="Screenshot 2023-02-23 at 2 44 10 PM" src="https://user-images.githubusercontent.com/122456892/220865272-0a8cdaeb-7992-4f87-b518-11ee934f0a2c.png">

## Solution 6:

SELECT mgr.FIRST_NAME,COUNT(*) as number_of_reporters
FROM emp_record_table emp JOIN emp_record_table mgr
ON emp.MANAGER_ID=mgr.EMP_ID
GROUP BY mgr.FIRST_NAME;


_Approach:-_

* Fetching the manager name _(employees whom other employees are reporting to)_ by _self joining_ the _emp_record_table_ with itself as manager is     also an employee with specific EMP_ID
* For first table I have given alias as _emp_ to emp_record_table and considering the same table as second table I have given alias as _mgr_

## OUTPUT:-
<img width="626" alt="Screenshot 2023-02-23 at 2 50 20 PM" src="https://user-images.githubusercontent.com/122456892/220866617-9f66494e-b705-4849-91ae-cbe504172a82.png">

## Solution 7:

* _Union_ returns all the _distinct rows_ between the data fetched by two select statements

SELECT EMP_ID,FIRST_NAME,LAST_NAME,DEPT - WHERE DEPT='HEALTHCARE'
UNION
SELECT EMP_ID,FIRST_NAME,LAST_NAME,DEPT
FROM emp_record_table WHERE DEPT='FINANCE';


_Approach:-_

* Here _First select_ statements fetch all the records _from the emp_record_table_ where _department is Healthcare_
* Union operator combines two select statements and gives distinct rows as result
* Here _Second select_ statements fetch all the records _from the emp_record_table_ where _department is FINANCE_

### OUTPUT:-

<img width="626" alt="Screenshot 2023-02-23 at 2 57 12 PM" src="https://user-images.githubusercontent.com/122456892/220868121-3cb5a086-697d-4598-bbf4-8f35eec179ca.png">

## Solution 8:

SELECT ert.EMP_ID, ert.FIRST_NAME, ert.LAST_NAME, ert.ROLE, ert.DEPT , ert.EMP_RATING,
MAX(ert.EMP_RATING) OVER(PARTITION BY ert.DEPT) as MAX_RATING_BY_DEPT
FROM emp_record_table ert;


_Approach:-_

* Fetching all the required columns asked from the emp_record_table 
* Using _window function_ to calculate _MAX of emp_rating partition by department_ FROM _emp_record_table_ ert; _(Considering ert as alias for       emp_record_table)_

### OUTPUT:-

<img width="718" alt="Screenshot 2023-02-23 at 3 39 09 PM" src="https://user-images.githubusercontent.com/122456892/220877797-aa9c8f57-0650-4326-aeed-2c10eb2c5431.png">

## Solution 9:

SELECT DISTINCT ROLE,
MAX(ert.SALARY) OVER(PARTITION BY ert.ROLE) AS max_salary, 
MIN(ert.SALARY) OVER(PARTITION BY ert.ROLE) AS min_salary 
FROM emp_record_table ert;


_Approach:-_

* In this question we have been asked to fetch the _minimum_ and _maximum_ salary of the employees based on each role, so I have used _window function to fetch the maximum and minimum using aggregate function max and min partition by ROLE(based on each role)_
* Used _DISTINCT Keyword_ here because _window funtion fetch the results in the form of frame_ ,so _duplicate data is returned_ based on the column fetched, so _to avoid redundant data_ I have used DISTINCT Keyword.

### OUTPUT:-
<img width="455" alt="Screenshot 2023-02-23 at 3 45 22 PM" src="https://user-images.githubusercontent.com/122456892/220878937-52c72f31-4f6d-4851-979e-1b5be2519389.png">

## Solution 10:

SELECT EMP_ID,EXP,
DENSE_RANK() OVER(ORDER BY EXP DESC) AS rnk 
FROM emp_record_table;


_Approach:-_

* Here I have used _DENSE_RANK()_ function to _assign ranks_ to the employees _based on their experience_
* _Window function_ will assign ranks using _DENSE_RANK order by experience from emp_record_table in descending order_ so that for _highest exp it will rank 1_ and so on.

### OUTPUT:-

<img width="455" alt="Screenshot 2023-02-23 at 3 50 19 PM" src="https://user-images.githubusercontent.com/122456892/220880291-0cce80d1-174d-4d7a-801a-11e66784566b.png">

## Solution 11:

CREATE OR REPLACE VIEW emp_salary_greater_than_six AS 
SELECT EMP_ID,FIRST_NAME,LAST_NAME,COUNTRY,SALARY FROM emp_record_table
WHERE SALARY > 6000;

select * from emp_salary_greater_than_six;


_Approach:-_

* Here I created a simple view called _emp_salary_greater_than_six_ which fetches all the records where _salary is greater than 6000_
* I have used _create_ or _replace_ because if _view already exists_ than _replace with the current content_ but if it _does not exists_ than
  _create a view with this content_.
  
### OUTPUT:-

<img width="455" alt="Screenshot 2023-02-23 at 3 58 01 PM" src="https://user-images.githubusercontent.com/122456892/220881679-ba3e8d88-455f-4718-b20e-33d3d8c214fd.png">

## Solution 12:

SELECT *
FROM emp_record_table
WHERE EXP IN (SELECT EXP FROM emp_record_table WHERE EXP > 10);


_Approach:-_

* In this particular question to use concept of nested query I have _first fetched the exp from the emp_record_table_ with the condition that _exp > 10_ which will _return all the exp greater than 10_ in the _WHERE CLAUSE_ of the outer select statement and from outer select statement I am fetching _all the records where exp matches with the result of the inner query_ and hence fetch employees with experience more than 10 years
  
### OUTPUT:-

<img width="1015" alt="Screenshot 2023-02-23 at 4 03 41 PM" src="https://user-images.githubusercontent.com/122456892/220882857-faf3523b-6dec-4dcc-9f38-86edbb6cbc0b.png">

## Solution 13:

* _NOTE: __Procedure_ is one of the _subprogram_ where we can store our query to _reuse later_ as and when required

DELIMITER $$
CREATE PROCEDURE employeeDetails() 
BEGIN
SELECT * 
FROM emp_record_table 
WHERE EXP > 3;
END $$ 
DELIMITER ;

CALL employeeDetails(); – To call the procedure


_Approach:-_
* Here I have created _Procedure name employeeDetails()_ which when called always _returns the details of employees with experience greater than 3_.

### OUTPUT:-
<img width="1019" alt="Screenshot 2023-02-23 at 4 09 03 PM" src="https://user-images.githubusercontent.com/122456892/220883866-a77a6a33-79b6-440c-8fa5-25393889a2ab.png">

## Solution 14:

DELIMITER $$
CREATE FUNCTION checkOrganizationStandard() RETURNS tinyint(1)
DETERMINISTIC
BEGIN
DECLARE finished INTEGER DEFAULT 0;
DECLARE v_exp INTEGER;
DECLARE v_role VARCHAR(50);

DECLARE expcursor
CURSOR FOR SELECT exp,role
           FROM data_science_team;
           
-- Declaring the handler to avoid the exception when cursor reaches the end of the row and their is no more rows to fetch
-- Setting finished to 1 which keeps a track of whether exception is generated
 or not, when it is set to 1we exit the loop and no more fetching is done
DECLARE CONTINUE HANDLER FOR NOT FOUND SET finished = 1;
OPEN expcursor;     -- To open the cursor
checkStandard:LOOP

FETCH expcursor INTO v_exp,v_role;
IF finished = 1 THEN LEAVE checkStandard;
END IF;


CASE v_exp
  WHEN v_exp <= 2 THEN
     IF v_role != 'JUNIOR DATA SCIENTIST' THEN 
        RETURN FALSE;
     END IF;
  WHEN v_exp > 2 and v_exp<=5 THEN
     IF v_role != 'ASSOCIATE DATA SCIENTIST' THEN 
        RETURN FALSE;
     END IF;
  WHEN v_exp > 5 and v_exp<=10 THEN
     IF v_role != 'SENIOR DATA SCIENTIST' THEN 
        RETURN FALSE; '
     END IF;
  WHEN v_exp > 10 and v_exp<=12 THEN
     IF v_role != 'LEAD DATA SCIENTIST' THEN 
        RETURN FALSE;
     END IF; 
  ELSE
     IF v_exp > 12 and v_exp<=16 AND v_role != 'MANAGER' THEN 
        RETURN FALSE
     END IF; 
END CASE;
END LOOP checkStandard; 
CLOSE expcursor;
RETURN TRUE; 
END $$ 
DELIMITER ;

 –- Created the procedure which will call the function created above and print
    the message 'Data matches the organization’s set standard' if function
    returns true otherwise 'Data does not matches the organization’s set
    standard' if it return false;

DELIMITER $$
CREATE PROCEDURE checkStandard(OUT res VARCHAR(20)) 
BEGIN
– Calling the function checkOrganizationStandard()
IF(checkOrganizationStandard()) THEN
   SET res= 'Data matches the organization’s set standard';
ELSE
   SET res='Data does not matches the organization’s set standard';
END IF; 
END $$

CALL checkStandard(@res); – Calling the Procedure 
SELECT @res as Result;


_Approach:-_

* Created the function _checkOrganizationStandard()_ which checks whether the job profile assigned to each employee in the data science team matches the
  _organization’s set standard_.
    * First Created the function with name checkOrganizationStandard with _Return type tinyint(1)_ as function return boolean value(True(1) or False(0))
    * Function is _Deterministic_ because it always gives the constant output for fixed set of inputs
    * Declare _finished variable_ which will be used later while handling exception to set it to 1 to exit the loop
    * Declaring _v_exp_ variable to fetch exp column data from _data_science_team_ while creating cursor
    * Declaring _v_role_ variable to fetch role column data from _data_science_team_ while creating cursor
    * Creating the _cursor with name expcursor_ which _fetches exp and role_ from _data_science_team_
    * Declaring the _handler_ to _avoid the exception_ when cursor reaches the _end of the row_ and their is no row to fetch
    * Setting finished to 1 which keeps a track of whether _exception is generated or not, when it is set to 1 we __exit_ the loop and no more
      fetching is done
    * Created Loop that will _fetch each row_ with the help of cursor and then _check the desired condition specified_ and accordingly gives the
      result
    * Fetching the data from the cursor into v_exp and v_role variable
    * In If Condition I checks for if no more rows are left,then exception is generated and finished is set to 1
    * whenever _finished=1_ condition satisfies we _break the loop_ as their is no more rows to traverse
    * Used _Case_ to check for _organization’s set standard_ as per the given question
	           * I have used the CASE over normal If because:- 
	                * A simple CASE statement is more readable and efficient than an IF statement when you compare a single expression against a range of 
	                     unique values.
                    
                       
             * if _v_exp is less than 2_ then it will hit this when statement where it will check for the _v_role if its 'JUNIOR DATA SCIENTIST',if   not it returns false because for the given __v_exp<=2_ role must be _'JUNIOR DATA SCIENTIST'_.
             * if _(2< v_exp <=5)_ then it will hit this when statement where it will check for the _v_role if its 'ASSOCIATE DATA SCIENTIST',  if   not it returns false because for the given _(2< v_exp <=5)_ role must be _'ASSOCIATE DATA SCIENTIST'__.
             * if _(5< v_exp <=10)_ then it will hit this when statement where it will check for the _v_role_ if its _'SENIOR DATA SCIENTIST',  if not it returns false because for the given _(5< v_exp <=10)_ role must be _'SENIOR DATA SCIENTIST'__.
             * if _(10< v_exp <=12)_ then it will hit this when statement where it will check for the _v_role_ if its _'LEAD DATA SCIENTIST',  if   not it returns false because for the given _(10 v_exp <=12)_ role must be _'LEAD DATA SCIENTIST'__.
             * else it will come in this block if none of above satisfies here it check if _(12<v_exp<=16)_ and _v_role_ is not manager then it return false because for the given range role must be _'MANAGER'_.
                       
    * Return True because if all the above condition in loop are not met none of the case returns false that means data is in accordance with
      organization’s set standard 
      
### OUTPUT:-
<img width="570" alt="Screenshot 2023-02-23 at 4 54 27 PM" src="https://user-images.githubusercontent.com/122456892/220892996-8a2cf654-8c64-4ed3-b304-e776d816dd06.png">

      
## Solution 15:

CREATE
INDEX index_first_name
ON emp_record_table(FIRST_NAME);

SELECT *
FROM emp_record_table WHERE FIRST_NAME='Eric';


_Approach:-_
* Here I am creating the _index_ on _FIRSTNAME_ attribute of _emp_record_table_ and then after i am fetching the record where _first_name_ is       'Eric'
* _Performance Analysis_
   
   * BEFORE CREATING INDEX THE QUERY TOOK 0.00061 sec
   * AFTER CREATING THE INDEX THE QUERY TOOK 0.00052 sec
   
* The _difference is not much as we have table with only 19 rows, so it __doesnt really have much impact_;

### OUTPUT:-
<img width="995" alt="Screenshot 2023-02-23 at 4 56 25 PM" src="https://user-images.githubusercontent.com/122456892/220893235-4b14cb30-6ed7-4953-aca1-f4e77f9418bd.png">

## Solution 16:

SELECT EMP_ID,EMP_RATING,SALARY,((0.05 * SALARY)*EMP_RATING) AS BONUS
FROM emp_record_table;


_Approach:-_
* Here getting the desired result by performing just the _airthmetic operation_ in select statement

### OUTPUT:-

<img width="494" alt="Screenshot 2023-02-23 at 5 04 05 PM" src="https://user-images.githubusercontent.com/122456892/220894725-4ff09d9f-4ec1-4b4e-a969-0e41badb21a4.png">

## Solution 17:

SELECT DISTINCT CONTINENT,
AVG(SALARY) OVER(PARTITION BY CONTINENT) AS avg_salary_by_continent,
COUNTRY,
AVG(SALARY) OVER(PARTITION BY COUNTRY) AS avg_salary_by_country FROM emp_record_table;


_Approach:-_
* Here I have used the _window function_ to get the _average salary by continent_ as well as _average salary by country_.

### OUTPUT:-

<img width="469" alt="Screenshot 2023-02-23 at 5 08 58 PM" src="https://user-images.githubusercontent.com/122456892/220895683-6c65d8f3-b356-4e6b-9aa7-b7dbbb353632.png">




### Srinivas's Way

### Question 1
Create a database named employee, then import data_science_team.csv proj_table.csv
and emp_record_table.csv into the employee database from the given resources.

<img width="291" alt="Screenshot 2023-02-22 at 3 43 06 PM" src="https://user-images.githubusercontent.com/122455311/220590095-e76e3153-5375-40d8-945a-9c8bfef166e9.png">

### Question 2
Create an ER diagram for the given employee database.

<img width="949" alt="Screenshot 2023-02-23 at 5 14 21 PM" src="https://user-images.githubusercontent.com/122455311/220896998-e3f3e93b-0d6e-4901-9ba6-e9c32c17084b.png">


### Question 3
Write a query to fetch EMP_ID, FIRST_NAME, LAST_NAME, GENDER, and DEPARTMENT from the employee record table, and make a list of employees and details of their department.

<img width="1000" alt="question3" src="https://user-images.githubusercontent.com/122455311/220598358-003e9828-1529-45fb-bcff-185e80a91f11.png">

### Question 4
Write a query to fetch EMP_ID, FIRST_NAME, LAST_NAME, GENDER, DEPARTMENT, and EMP_RATING if the EMP_RATING is:
- less than two

<img width="835" alt="question4a" src="https://user-images.githubusercontent.com/122455311/220598573-2ceb6135-f190-4670-aba3-666c860d5dc7.png">

- greater than four

<img width="904" alt="question4b" src="https://user-images.githubusercontent.com/122455311/220598629-2ab96032-7a1e-497a-94e5-279b389377f7.png">

- between two and four

<img width="891" alt="question4c" src="https://user-images.githubusercontent.com/122455311/220598695-4f26d2d3-dab4-432d-a05e-6f3858563d41.png">

### Question 5
Write a query to concatenate the FIRST_NAME and the LAST_NAME of employees in the Finance department from the employee table and then give the resultant column alias as NAME.

<img width="1050" alt="question5" src="https://user-images.githubusercontent.com/122455311/220598754-74d11928-b220-4e92-9b71-d0e2574ba22c.png">

### Question 6
Write a query to list only those employees who have someone reporting to them. Also, show the number of reporters (including the President).

<img width="1076" alt="question6" src="https://user-images.githubusercontent.com/122455311/220598889-06203bc1-299e-42fb-a14e-fdbfa7930f70.png">

### Question 7
Write a query to list down all the employees from the healthcare and finance departments using union. Take data from the employee record table.

<img width="1086" alt="question7" src="https://user-images.githubusercontent.com/122455311/220598975-c02e53e7-153c-43c4-b582-f24badf4132d.png">

### Question 8
Write a query to list down employee details such as EMP_ID, FIRST_NAME, LAST_NAME, ROLE, DEPARTMENT, and EMP_RATING grouped by dept. Also include the respective employee rating along with the max emp rating for the department.

<img width="1083" alt="question8" src="https://user-images.githubusercontent.com/122455311/220599061-5342e4a6-09e8-45a6-90b5-7e1828cb13f5.png">

### Question 9
Write a query to calculate the minimum and the maximum salary of the employees in each role. Take data from the employee record table.

<img width="825" alt="question9" src="https://user-images.githubusercontent.com/122455311/220599145-7b5cf1c8-6740-4928-9515-2b40079403ec.png">

### Question 10
Write a query to assign ranks to each employee based on their experience. Take data from the employee record table.

<img width="1098" alt="question10" src="https://user-images.githubusercontent.com/122455311/220599231-0e0d1f6a-d2ef-41bf-be42-c1a92facd2ed.png">

### Question 11
Write a query to create a view that displays employees in various countries whose salary is more than six thousand. Take data from the employee record table.

<img width="1144" alt="question11" src="https://user-images.githubusercontent.com/122455311/220599303-699ae791-2332-46e2-aecb-ed067c7b57a0.png">

### Question 12
Write a nested query to find employees with experience of more than ten years. Take data from the employee record table.

<img width="1077" alt="question12" src="https://user-images.githubusercontent.com/122455311/220599412-6bd17a8d-8768-479f-bae3-3df966afb08e.png">

### Question 13
Write a query to create a stored procedure to retrieve the details of the employees whose experience is more than three years. Take data from the employee record table.

<img width="1079" alt="question13" src="https://user-images.githubusercontent.com/122455311/220599492-6e558350-1310-43a5-8607-67b8d59caef8.png">

### Question 14
 Write a query using stored functions in the project table to check whether the job profile assigned to each employee in the data science team matches the organization’s set standard.
 The standard being:
- For an employee with experience less than or equal to 2 years assign 'JUNIOR DATA SCIENTIST', For an employee with the experience of 2 to 5 years assign 'ASSOCIATE DATA SCIENTIST',
- For an employee with the experience of 5 to 10 years assign 'SENIOR DATA SCIENTIST',
- For an employee with the experience of 10 to 12 years assign 'LEAD DATA SCIENTIST',
- For an employee with the experience of 12 to 16 years assign 'MANAGER'
 
 <img width="1145" alt="question14" src="https://user-images.githubusercontent.com/122455311/220599590-ef9a0909-e3c3-4c41-a9bc-d4d26bc63bdb.png">

### Question 15
Create an index to improve the cost and performance of the query to find the employee whose FIRST_NAME is ‘Eric’ in the employee table after checking the execution plan.

<img width="1152" alt="question15" src="https://user-images.githubusercontent.com/122455311/220599771-066f12c7-c466-4aa3-a05a-8e8af7ffce5c.png">

### Question 16
Write a query to calculate the bonus for all the employees, based on their ratings and salaries (Use the formula: 5% of salary * employee rating).

<img width="1039" alt="question16" src="https://user-images.githubusercontent.com/122455311/220599839-80a25af5-cfb4-42e6-b5de-f7e9148422fc.png">

### Question 17
Write a query to calculate the average salary distribution based on the continent and country. Take data from the employee record table.

<img width="1036" alt="question17" src="https://user-images.githubusercontent.com/122455311/220599920-8d7ae935-5a1a-42bb-9927-68e5157bd5c4.png">
