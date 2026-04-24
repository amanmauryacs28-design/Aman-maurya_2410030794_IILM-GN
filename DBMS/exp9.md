# Experiment 9: SQL Subqueries and Nested Queries

## Aim
To perform SQL queries using subqueries and nested SELECT statements on EMPLOYEE table.

## Queries

```sql
-- 1. Display the name of employee who earns highest salary
SELECT ENAME
FROM EMPLOYEE
WHERE SAL = (SELECT MAX(SAL) FROM EMPLOYEE);

-- 2. Display the employee number and name of employee working as clerk and earning highest salary among clerks
SELECT EMPNO, ENAME
FROM EMPLOYEE
WHERE JOB='CLERK'
AND SAL = (SELECT MAX(SAL) FROM EMPLOYEE WHERE JOB='CLERK');

-- 3. Display the names of salesman who earn salary more than highest salary of any clerk
SELECT ENAME
FROM EMPLOYEE
WHERE JOB='SALESMAN'
AND SAL > (SELECT MAX(SAL) FROM EMPLOYEE WHERE JOB='CLERK');

-- 4. Display the names of clerks who earn salary more than James and salary less than Scott
SELECT ENAME
FROM EMPLOYEE
WHERE JOB='CLERK'
AND SAL > (SELECT SAL FROM EMPLOYEE WHERE ENAME='JAMES')
AND SAL < (SELECT SAL FROM EMPLOYEE WHERE ENAME='SCOTT');

-- 5. Display the names of employees who earn salary more than James or salary greater than Scott
SELECT ENAME
FROM EMPLOYEE
WHERE SAL > (SELECT SAL FROM EMPLOYEE WHERE ENAME='JAMES')
OR SAL > (SELECT SAL FROM EMPLOYEE WHERE ENAME='SCOTT');

-- 6. Display the names of employees who earn highest salary in their respective departments
SELECT ENAME
FROM EMPLOYEE E
WHERE SAL = (
SELECT MAX(SAL)
FROM EMPLOYEE
WHERE DEPTNO = E.DEPTNO
);

-- 7. Display the names of employees who earn highest salaries in their respective job groups
SELECT ENAME
FROM EMPLOYEE E
WHERE SAL = (
SELECT MAX(SAL)
FROM EMPLOYEE
WHERE JOB = E.JOB
);

-- 8. Display the employee names who are working in accounting department
SELECT ENAME
FROM EMPLOYEE
WHERE DEPTNO = (
SELECT DEPTNO
FROM DEPARTMENT
WHERE DNAME='ACCOUNTING'
);

-- 9. Display the employee names who are working in Chicago
SELECT ENAME
FROM EMPLOYEE
WHERE DEPTNO = (
SELECT DEPTNO
FROM DEPARTMENT
WHERE LOC='CHICAGO'
);

-- 10. Display the job groups having total salary greater than maximum salary for managers
SELECT JOB
FROM EMPLOYEE
GROUP BY JOB
HAVING SUM(SAL) >
(
SELECT MAX(SAL)
FROM EMPLOYEE
WHERE JOB='MANAGER'
);