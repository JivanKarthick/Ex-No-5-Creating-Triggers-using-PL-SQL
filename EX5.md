# Ex. No: 5 Creating Triggers using PL/SQL

### AIM: To create a Trigger using PL/SQL.

### Steps:
1. Create employee table with following attributes (empid NUMBER, empname VARCHAR(10), dept VARCHAR(10),salary NUMBER);
2. Create salary_log table with following attributes (log_id NUMBER GENERATED ALWAYS AS IDENTITY, empid NUMBER,empname VARCHAR(10),old_salary NUMBER,new_salary NUMBER,update_date DATE);
3. Create a trigger named as log_salary-update.
4. Inside the trigger block, Insert the values into the salary_log table whenever the salary is updated.
5. End the trigger.
6. Update the salary of an employee in employee table.
7. Whenever a salary is updated for the employee it must be logged into the salary_log table with old salary and new salary.
8. Display the employee table, salary_log table.

### Program:
### Create employee table
```
CREATE TABLE employedd(
  empid NUMBER,
  empname VARCHAR2(10),
  dept VARCHAR2(10),
  salary NUMBER
);

CREATE TABLE sal_logg (
  log_id NUMBER GENERATED ALWAYS AS IDENTITY,
  empid NUMBER,
  empname VARCHAR2(10),
  old_salary NUMBER,
  new_salary NUMBER,
  update_date DATE
);
-- Insert the values in the employee table
insert into employedd values(1,'gojo','IT',1000000);
insert into employedd values(2,'Sojo','SALES',500000)
```
### Create employee table
![image](https://github.com/JivanKarthick/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/121165867/518d8d34-4b8c-404f-ab03-967bb207217e)


### Create salary_log table
![image](https://github.com/JivanKarthick/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/121165867/a8db6f05-1df9-4b9a-aeed-cf19d06e86c0)




### PLSQL Trigger code
```
-- Create the trigger
CREATE OR REPLACE TRIGGER logg_sal_update
BEFORE UPDATE ON employedd
FOR EACH ROW
BEGIN
  IF :OLD.salary != :NEW.salary THEN
    INSERT INTO sal_logg (empid, empname, old_salary, new_salary, update_date)
    VALUES (:OLD.empid, :OLD.empname, :OLD.salary, :NEW.salary, SYSDATE);
  END IF;
END;
/
-- Insert the values in the employee table
insert into employed values(2,'Sojo','SALES',500000);
insert into employedd values(1,'gojo','IT',1000000);

-- Update the salary of an employee
UPDATE employedd
SET salary = 600000
WHERE empid=2;
-- Display the employee table
SELECT * FROM employedd;

-- Display the salary_log table
SELECT * FROM sal_logg;
```
### Output:

![image](https://github.com/JivanKarthick/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/121165867/b8b72ac9-02a5-460a-9752-f6f039526c68)


### Result:
Thus the program implemented successfully.
