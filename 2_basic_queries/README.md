## Basic SQL Queries

```sql
-- Q0
-- Retrieve the birth date and address of the employee(s) whose name is ‘John B. Smith’.
SELECT BDATE, Address
FROM EMPLOYEE
WHERE FName='John' AND Minit='B' AND LName='Smith';

-- Q1
-- Retrieve the name and address of all employees who work for the ‘Research’ department. 
Q1: 
SELECT FName, LName, Address
FROM EMPLOYEE, DEPARTMENT
WHERE Dname='Research' AND Dnumber=Dno;
/

-- Q2
-- For every project located in ‘Stafford’, list the project number, the controlling department number, and the department manager’s last name, address, and birth date. 
SELECT Pnumber, Dnum, Lname, Address, Bdate
FROM PROJECT, EMPLOYEE, DEPARTMENT 
WHERE Plocation=‘Stafford’ AND DNUM=Dnumber AND MGR_SSN=SSN

-- Q3
-- For each employee, retrieve the employee’s first and last name and the first and last name of his or her immediate supervisor. 
SELECT E.FName, E.LName, S.FName, S.LName 
FROM EMPLOYEE E, EMPLOYEE S
WHERE E.super_ssn=S.ssn;

-- Q4
-- Select all EMPLOYEE SSNs
SELECT SSN
FROM EMPLOYEE;

-- Q5
-- Select all combinations of EMPLOYEE Ssn and DEPARTMENT Dname in the database.
SELECT SSN, DNAME
FROM EMPLOYEE, DEPARTMENT

-- Q6
-- Compinations of all rows with all attributes in EMPLOYEE and DEPARTMENT
SELECT *
FROM EMPLOYEE, DEPARTMENT;

-- Q7
-- Retrieve the salary of every employee (Q7) and all distinct salary values (Q7A).
SELECT ALL Salary
FROM EMPLOYEE;
/

-- Q7A
-- Retrieve the salary of every employee (Q7) and all distinct salary values (Q7A).
SELECT DISTINCT Salary
FROM EMPLOYEE;
/ 

-- Q8 (Tables as Sets)
-- Make a list of all project numbers for projects that involve an employee whose last name is ‘Wong’, either as a worker or as a manager of the department that controls the project.

(SELECT DISTINCT Pnumber
FROM PROJECT, DEPARTMENT, EMPLOYEE
WHERE Dnum=Dnumber AND Mgr_ssn = Ssn AND Lname= 'Wong')
UNION
(SELECT DISTINCT Pnumber
FROM PROJECT, WORKS_ON, EMPLOYEE
WHERE Pnumber=Pno AND Essn=Ssn AND Lname ='Wong')

-- Substring 
SELECT *
FROM EMPLOYEE 
WHERE Ssn LIKE '__8__5555'; 

SELECT *
FROM EMPLOYEE 
WHERE Address LIKE ‘%Houston TX%’; 

-- Between Operator 
SELECT *
FROM EMPLOYEE 
WHERE(Salary BETWEEN 30000 AND 40000) AND Dno = 5; 

-- Arithmetic Operations
SELECT E.FName, E.LName, 1.1*E.Salary AS Increased_Sal
FROM EMPLOYEE E, WORKS_ON W, PROJECT P
WHERE P.Pname='ProductX' AND W.Pno=P.Pnumber AND E.Ssn=W.Essn;

-- Insert
INSERT INTO EMPLOYEE VALUES ('Naren', 'P', 'Khatwani', '999001111', TO_DATE('1988-08-15', 'YYYY-MM-DD'), '123 Spruce St, Plano TX', 'M', 48000, '333445555', 5);

-- Bulk Loading
CREATE TABLE D5EMPS AS (SELECT E.*FROM EMPLOYEE E WHERE E.Dno=5); 

-- View Bulk Loading
Select * 
From D5EMPS;

-- Drop Table
DROP TABLE D5EMPS;

-- Update
UPDATE EMPLOYEE
SET Address = 'Jersey City, NJ'
WHERE Fname = 'Naren' AND Lname = 'Khatwani' AND Ssn = '999001111';

-- Delete
DELETE FROM EMPLOYEE
WHERE Fname = 'Naren' AND Lname = 'Khatwani';
```