# SQL-CASE-STUDY-
Create the following table: 
LOCATION 
Location_ID(PK) 	 City 
122	New York
123	Dallas
124	Chicago
167	Boston
Department
Department_Id(PK)	Name	Location_Id(FK)
10	Accounting	122
20	Sales	124
30	Research	123
40	Operations	167
JOB
Job_ID(PK)	Designation
667	Clerk
668	Staff
669	Analyst
670	Sales Person
671	Manager
672	President
EMPLOYEE
Employee_Id	Last_Name	First_Name	Middle_ Name	Job_Id( FK)	Hire Date	Salary	Comm	Department_Id(FK)
7369	Smith	John	Q	667	17-Dec-84	800	Null	20
7499	Allen	Kevin	J	670	20-Feb-85	1600	300	30
755	Doyle	Jean	K	671	04-Apr-85	2850	Null	30
756	Dennis	Lynn	S	671	15-May-85	2750	Null	30
757	Baker	Leslie	D	671	10-Jun-85	2200	Null	40
7521	Wark	Cynthia	D	670	22-Feb-85	1250	50	30


CREATE DATABASE SAMIM_CASESTUDY2
GO

USE SAMIM_CASESTUDY2
GO

---Create tables as per the data

CREATE TABLE LOCATION (
    Location_ID INT NOT NULL,
    City VARCHAR(50),
    PRIMARY KEY (Location_ID))

CREATE TABLE DEPARTMENT (
     Department_ID INT PRIMARY KEY,
	 Name VARCHAR(50),
	 Location_ID INT,
	 FOREIGN KEY (Location_ID) REFERENCES Location(Location_ID))

CREATE TABLE JOB (
     Job_ID INT PRIMARY KEY,
	 Designation VARCHAR(50))

CREATE TABLE EMPLOYEE
(EMPLOYEE_ID INT,
LAST_NAME VARCHAR(20),
FIRST_NAME VARCHAR(20),
MIDDLE_NAME CHAR(1),
JOB_ID INT FOREIGN KEY
REFERENCES JOB(JOB_ID),
MANAGER_ID INT,
HIRE_DATE DATE,
SALARY INT,
COMM INT,
DEPARTMENT_ID  INT FOREIGN KEY
REFERENCES DEPARTMENT(DEPARTMENT_ID))


---Insert DATA in the above tables

INSERT INTO LOCATION (Location_ID, City)
VALUES (122, 'New York'),
       (123, 'Dallas'),
       (124, 'Chicago'),
       (167, 'Boston')

INSERT INTO DEPARTMENT (Department_Id, Name, Location_Id)
VALUES (10, 'Accounting', 122),
       (20, 'Sales', 124),
       (30, 'Research', 123),
       (40, 'Operations', 167)


INSERT  INTO JOB VALUES
(667, 'CLERK'),
(668,'STAFF'),
(669,'ANALYST'),
(670,'SALES_PERSON'),
(671,'MANAGER'),
(672, 'PRESIDENT')

INSERT INTO EMPLOYEE VALUES
(7369,'SMITH','JOHN','Q',667,7902,'17-DEC-84',800,NULL,20),
(7499,'ALLEN','KEVIN','J',670,7698,'20-FEB-84',1600,300,30),
(7505,'DOYLE','JEAN','K',671,7839,'04-APR-85',2850,NULl,30),
(7506,'DENNIS','LYNN','S',671,7839,'15-MAY-85',2750,NULL,30),
(7507,'BAKER','LESLIE','D',671,7839,'10-JUN-85',2200,NULL,40),
(7521,'WARK','CYNTHIA','D',670,7698,'22-FEB-85',1250,500,30)



---Simple Queries

---1.List all the employee details.

SELECT * FROM EMPLOYEE

---2.List all the department details.

SELECT * FROM DEPARTMENT

---3.List all job details.

SELECT * FROM JOB

---4.List all the locations.

SELECT * FROM LOCATION


---5.List out the First Name,Last Name,Salary, Commission for all Employees.

SELECT First_Name,Last_Name,CONCAT(First_Name,' ',Last_Name) AS Full_Name,SALARY,COMM FROM EMPLOYEE


---6. List out the Employee ID, Last Name, Department ID for all employees and alias
---Employee ID as "ID of the Employee", Last Name as "Name of the Employee", Department ID as "Dep_id".

SELECT Employee_ID AS "ID of The Employee",
Last_Name AS "Name of The Employee",
Department_ID AS "The Dep_id"
FROM Employee


---7. List out the annual salary of the employees with their names only.

SELECT CONCAT(First_Name,' ',Last_Name) AS Full_Name, Salary FROM EMPLOYEE

---WHERE Condition

---1. List the details about "Smith"

SELECT * FROM EMPLOYEE WHERE LAST_NAME = 'Smith'

---2.List out the employees who are working in department20.

SELECT * FROM EMPLOYEE WHERE DEPARTMENT_ID = 20

---3. List out the employees who are earning salaries between 3000 and4500.

SELECT * FROM EMPLOYEE WHERE SALARY BETWEEN 3000 AND 4500

---4. List out the employees who are working in department 10 or 20

SELECT * FROM EMPLOYEE WHERE DEPARTMENT_ID IN (10, 20)

---5. Find out the employees who are not working in department 10 or 30.

SELECT * FROM EMPLOYEE WHERE DEPARTMENT_ID IN (10, 30)

---6. List out the employees whose name starts with 'S'

SELECT  * FROM EMPLOYEE WHERE FIRST_NAME LIKE 's%'

---7. List out the employees whose name starts with 'S' and ends with 'H'

SELECT * FROM EMPLOYEE
WHERE FIRST_NAME LIKE 'S%H'

---8. List out the employees whose name length is 4 and starts with 'S'.

SELECT Employee_ID, FIRST_NAME
FROM Employee
WHERE FIRST_NAME LIKE 'S___'

---9.List out employees who are working in department 10 and draw salaries more than 3500.

SELECT Employee_ID FROM EMPLOYEE 
WHERE DEPARTMENT_ID=10 AND SALARY >3500

---10. List out the employees who are not receiving commission.

SELECT * FROM EMPLOYEE 
WHERE Comm IS NULL


---ORDER BY Clause

---1. List out the Employee ID and Last Name in ascending order based on the Employee ID.

SELECT EMPLOYEE_ID,LAST_NAME FROM  EMPLOYEE
ORDER BY EMPLOYEE_ID ASC


---2. List out the Employee ID and Name in descending order base.

SELECT EMPLOYEE_ID, CONCAT(First_Name,' ',Last_Name) AS Full_Name 
FROM EMPLOYEE ORDER BY EMPLOYEE_ID,Full_Name DESC


---3. List out the employee details according to their Last Name in ascending-order.
SELECT * FROM EMPLOYEE 
ORDER BY LAST_NAME

---4. List out the employee details according to their Last Name in ascending order and then Department ID in descendinG order.

SELECT * FROM EMPLOYEE 
ORDER BY LAST_NAME, DEPARTMENT_ID DESC


---GROUP BY and HAVING Clause:

---1. How many employees are in different departments in the organization?

SELECT DEPARTMENT_ID,COUNT(*) AS Employee_Count
FROM EMPLOYEE
GROUP BY DEPARTMENT_ID

---2. List out the department wise maximum salary, minimum salary and average salary of the employees. 

SELECT Department_ID,
MAX(Salary) AS Maximum_Salary,
MIN(Salary) AS Minimum_Salary,
AVG(Salary) AS Average_Salary
FROM EMPLOYEE
GROUP BY DEPARTMENT_ID


---3. List out the job wise maximum salary, minimum salary and average salary of the employees.

SELECT JOB_ID,
MAX(Salary) AS Maximum_Salary,
MIN(Salary) AS Minimum_Salary,
AVG(Salary) AS Average_Salary
FROM EMPLOYEE
GROUP BY Job_ID


---4. List out the number of employees who joined each month in ascendingorder. 

SELECT HIRE_DATE,COUNT(*) FROM EMPLOYEE
GROUP BY HIRE_DATE
ORDER BY HIRE_DATE ASC


---5. List out the number of employees for each month and year in ascending order based on the year and month. 

SELECT 
    YEAR(HIRE_DATE) AS JoinYear, 
    MONTH(HIRE_DATE) AS JoinMonth, 
    COUNT(*) AS NumberOfEmployees
FROM 
    Employee
GROUP BY 
    YEAR(HIRE_DATE), MONTH(HIRE_DATE)
ORDER BY 
    YEAR(HIRE_DATE) ASC, MONTH(HIRE_DATE) ASC

---6. List out the Department ID having at least four employees. 

SELECT DEPARTMENT_ID FROM EMPLOYEE
HAVING COUNT (*) > 4


---7. How many employees joined in the month of January?

SELECT COUNT(*) AS NumberOfEmployees
FROM Employee
WHERE MONTH(HIRE_DATE) = 1


---8. How many employees joined in the month of January orSeptember?

SELECT COUNT(*) AS NumberOfEmployees
FROM Employee
WHERE MONTH(HIRE_DATE) = 1 OR 9


---9. How many employees joined in 1985?

SELECT COUNT(*) AS NumberOfEmployees
FROM Employee
WHERE YEAR(HIRE_DATE) = 1985

---10. How many employees joined each month in 1985?

SELECT MONTH (Hire_Date) AS Join_Month,
COUNT(*) AS Number_OF_Employees
FROM EMPLOYEE
WHERE YEAR(HIRE_DATE)=1985
GROUP BY MONTH(HIRE_DATE)
ORDER BY MONTH(HIRE_DATE)


---11. How many employees joined in March 1985?


SELECT MONTH (Hire_Date) AS Join_Month,
COUNT(*) AS Number_OF_Employees
FROM EMPLOYEE
WHERE YEAR(HIRE_DATE)=1985
GROUP BY MONTH(HIRE_DATE)
ORDER BY MONTH(HIRE_DATE)


---12. Which is the Department ID having greater than or equal to 3 employees joining in April 1985?

SELECT COUNT(*) AS NumberOfEmployees
FROM EMPLOYEE
WHERE MONTH(HIRE_DATE) = 3 AND YEAR(HIRE_DATE) = 1985

---JOINS


---1. List out employees with their department names.

SELECT EMPLOYEE.EMPLOYEE_ID,EMPLOYEE.FIRST_NAME,EMPLOYEE.LAST_NAME,DEPARTMENT.Name FROM EMPLOYEE
JOIN DEPARTMENT ON EMPLOYEE.DEPARTMENT_ID=DEPARTMENT.Department_ID

---2. Display employees with their designations. 

SELECT EMPLOYEE.EMPLOYEE_ID,EMPLOYEE.FIRST_NAME,EMPLOYEE.LAST_NAME,JOB.Designation FROM EMPLOYEE
JOIN JOB ON EMPLOYEE.JOB_ID=JOB.Job_ID


---3. Display the employees with their department names and regional groups.

SELECT EMPLOYEE.EMPLOYEE_ID,EMPLOYEE.FIRST_NAME,EMPLOYEE.LAST_NAME,DEPARTMENT.Name, LOCATION.City FROM EMPLOYEE
JOIN DEPARTMENT ON EMPLOYEE.DEPARTMENT_ID=DEPARTMENT.Department_ID
JOIN LOCATION ON DEPARTMENT.LOCATION_ID=LOCATION.LOCATION_ID



---4. How many employees are working in different departments? Display with department names.

SELECT Department.Department_ID,
    Department.Name AS Department_Name,
    COUNT(Employee.Employee_ID) AS Employee_Count
    FROM Department
    LEFT JOIN
    Employee ON Department.Department_ID = Employee.Department_ID
    GROUP BY
    Department.Department_ID, Department.Name


---5. How many employees are working in the sales department?

SELECT COUNT(Employee.Employee_ID) AS Sales_Department_Employee_Count
    FROM Employee
    JOIN Department ON Employee.Department_ID = Department.Department_ID
    WHERE Department.Name = 'Sales'

---6. Which is the department having greater than or equal to 5employees? Display the department names in ascending order. 

SELECT Department.Name AS Department_Name,
    COUNT(Employee.Employee_ID) AS Employee_Count
    FROM Department
    LEFT JOIN Employee ON Department.Department_ID = Employee.Department_ID
    GROUP BY Department.Department_ID, Department.Name
    HAVING COUNT(Employee.Employee_ID) >= 5
    ORDER BY Employee_Count ASC;


---7. How many jobs are there in the organization? Display with designations. 

SELECT COUNT(DISTINCT job_ID) AS Total_Jobs, Job_ID, Designation
    FROM JOB
    GROUP BY Job_ID, Designation


---8. How many employees are working in "New York"?

SELECT COUNT(Employee.Employee_ID) AS Employees_In_NewYork
FROM Employee
JOIN Department ON Employee.Department_ID = Department.Department_ID
JOIN Location ON Department.Location_ID = Location.Location_ID
WHERE Location.City = 'New York'  


---9. Display the employee details with salary grades. Use conditional statementto create a grade column. 

SELECT
    EMPLOYEE.employee_ID,
    EMPLOYEE.Last_Name,
    EMPLOYEE.Salary,
    LOCATION.City,
    DEPARTMENT.Name AS Department_Name,
    CASE
        WHEN EMPLOYEE.Salary >= 80000 THEN 'Grade A'
        WHEN EMPLOYEE.Salary BETWEEN 60000 AND 79999 THEN 'Grade B'
        WHEN EMPLOYEE.Salary BETWEEN 40000 AND 59999 THEN 'Grade C'
        ELSE 'Grade D'
    END AS Salary_Grade
    FROM EMPLOYEE 
    JOIN Department  ON EMPLOYEE.Department_ID = DEPARTMENT.Department_ID
    JOIN Location  ON DEPARTMENT.Location_ID = LOCATION.Location_ID


---10. List out the number of employees grade wise. Use conditional statementto create a grade column. 

SELECT
    CASE
        WHEN Salary >= 80000 THEN 'Grade A'
        WHEN Salary BETWEEN 60000 AND 79999 THEN 'Grade B'
        WHEN Salary BETWEEN 40000 AND 59999 THEN 'Grade C'
        ELSE 'Grade D'
        END AS Salary_Grade,
        COUNT(EMPLOYEE_ID) AS Employee_Count
        FROM EMPLOYEE
        GROUP BY Salary



---11.Display the employee salary grades and the number of employees between 2000 to 5000 range of salary. 

SELECT
     CASE
     WHEN Salary >= 80000 THEN 'Grade A'
     WHEN Salary BETWEEN 60000 AND 79999 THEN 'Grade B'
     WHEN Salary BETWEEN 40000 AND 59999 THEN 'Grade C'
     ELSE 'Grade D'
     END AS Salary_Grade,
     COUNT(employee_ID) AS Employee_Count
     FROM EMPLOYEE
     WHERE Salary BETWEEN 2000 AND 5000
     GROUP BY Salary


---12. Display all employees in sales or operation department

SELECT
    EMPLOYEE.Employee_ID,
    EMPLOYEE.Last_Name,
    EMPLOYEE.Job_ID,
    Department.Name AS Department_Name
    FROM EMPLOYEE
    JOIN DEPARTMENT  ON EMPLOYEE.Department_ID = DEPARTMENT.Department_ID
    WHERE DEPARTMENT.Name IN ('Sales', 'Operation')



---SET Operators:


---1. List out the distinct jobs in sales and accounting departments.

SELECT DISTINCT Job.Designation
FROM Employee
JOIN Department ON Employee.Department_ID = Department.Department_ID
JOIN Job ON Employee.Job_ID = Job.Job_ID
WHERE Department.Name = 'Sales'
UNION
SELECT DISTINCT Job.Designation
FROM Employee
JOIN Department ON Employee.Department_ID = Department.Department_ID
JOIN Job ON Employee.Job_ID = Job.Job_ID
WHERE Department.Name = 'Accounting'


---2. List out all the jobs in sales and accounting departments. 

SELECT DISTINCT Job.Designation
FROM Employee
JOIN Department ON Employee.Department_ID = Department.Department_ID
JOIN Job ON Employee.Job_ID = Job.Job_ID
WHERE Department.Name IN ('Sales', 'Accounting')



---3. List out the common jobs in research and accounting departments in ascending order.

SELECT Job.Designation
FROM Employee
JOIN Department ON Employee.Department_ID = Department.Department_ID
JOIN Job ON Employee.Job_ID = Job.Job_ID
WHERE Department.Name = 'Research'
INTERSECT
SELECT Job.Designation
FROM Employee
JOIN Department ON Employee.Department_ID = Department.Department_ID
JOIN Job ON Employee.Job_ID = Job.Job_ID
WHERE Department.Name = 'Accounting'
ORDER BY Job.Designation ASC



---Subqueries


---1. Display the employees list who got the maximum salary.

SELECT * FROM Employee
WHERE Salary IN (SELECT MAX(Salary) AS Maximum_Salary FROM Employee)

---2. Display the employees who are working in the sales department.

SELECT * FROM EMPLOYEE
WHERE Department_ID = (SELECT Department_ID FROM Department WHERE Name = 'Sales')


---3. Display the employees who are working as 'Clerk'.

SELECT * FROM EMPLOYEE 
WHERE JOB_ID= (SELECT JOB_ID FROM JOB WHERE Designation= 'Clerk')

---4. Display the list of employees who are living in "New York".


SELECT EMPLOYEE.* FROM EMPLOYEE
JOIN DEPARTMENT ON EMPLOYEE.DEPARTMENT_ID=DEPARTMENT.Department_ID
JOIN LOCATION ON DEPARTMENT.Location_ID=LOCATION.Location_ID
WHERE Location.City='New York'


---5. Find out the number of employees working in the sales department.

SELECT COUNT(*) AS Sales_Department_Employee_Count
FROM Employee
JOIN Department ON Employee.Department_ID = Department.Department_ID
WHERE Department.Name = 'Sales'

---6. Update the salaries of employees who are working as clerks on the basis of 10%


UPDATE EMPLOYEE
SET SALARY = SALARY * 1.1
WHERE JOB_ID= (SELECT JOB_ID FROM JOB WHERE Designation='Clerk')


---7. Delete the employees who are working in the accounting.

DELETE FROM Employee
WHERE Department_ID = (SELECT Department_ID FROM Department WHERE Name = 'Accounting')

---8. Display the second highest salary drawing employee details.

SELECT * FROM Employee
WHERE Salary = (SELECT MAX(Salary)
    FROM Employee
    WHERE Salary < (SELECT MAX(Salary) FROM Employee)
)

---9.	Display the nth highest salary drawing employee details.

---Consider nth=5

WITH SalaryRanking AS (
    SELECT *,
           DENSE_RANK() OVER (ORDER BY Salary DESC) AS Rank
    FROM Employee
)
SELECT *
FROM SalaryRanking
WHERE Rank = 5

---10.	List out the employees who earn more than every employee in  department 30.

SELECT * FROM Employee
WHERE Salary > ALL (SELECT Salary FROM Employee WHERE Department_ID = 30)

---11.	List out the employees who earn more than the lowest salary in department. Find out whose department has no employees.

--- Employees earning more than the lowest salary in their department

SELECT EMPLOYEE.* FROM Employee 
WHERE Salary > (SELECT MIN(Salary) FROM Employee WHERE Department_ID = EMPLOYEE.Department_ID);

-- Departments with no employees
SELECT Department.* FROM Department 
WHERE NOT EXISTS (SELECT 1 FROM Employee WHERE Department_ID = DEPARTMENT.Department_ID);

---12.	Find out which department has no employees.

SELECT Department.* FROM Department
LEFT JOIN Employee ON Department.Department_ID = Employee.Department_ID
WHERE Employee.Employee_ID IS NULL

---13.	Find out the employees who earn greater than the average salary for their department.

SELECT Employee.* FROM Employee
WHERE Salary > (SELECT AVG(Salary)
    FROM Employee AS HIGH_EARNING_EMPLOYEE
    WHERE HIGH_EARNING_EMPLOYEE.Department_ID = Employee.Department_ID
)
