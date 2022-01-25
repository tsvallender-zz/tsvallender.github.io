---
---
SQL
Table manipulation
CREATE TABLE employee (
    employee_id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(40) NOT NULL,
    role VARCHAR(20) DEFAULT 'Starter',
);
Other keywords: UNIQUE
FOREIGN KEY(mgr_id) REFERENCES employee(employee_id) ON DELETE SET NULL;
DESCRIBE employee;
DROP TABLE employee;
ALTER TABLE employee ADD rate DECIMAL(8, 2);
ALTER TABLE employee DROP COLUMN rate;
ALTER TABLE employee ADD FOREIGN KEY(mgr_id) REFERENCES employee(employee_id) ON DELETE SET NULL;
PRIMARY KEY(col1, col2) for composite PK.
ON DELETE CASCADE to cascade deletes
Query
SELECT name, age
FROM employee
WHERE salary > 3000;
SELECT * FROM employee
ORDER BY rate, role ASC
LIMIT 6;
Not equal is <>
SELECT * FROM employee
WHERE name IN ('Dave', 'Chris');
SELECT DISTINCT rate FROM employee;
WHERE name LIKE '';
% any no of chars
_ one char
SELECT employee.name, MAX(rate) FROM employee
LIMIT 1 OFFSET 2 -- third row
Joins
SELECT employee.id, employee.name, branch.name
FROM employee
JOIN branch
ON employee.id = branch.mgr_id;
LEFT JOIN includes includes all rows from left table, even those that don't match the right. RIGHT JOIN does the opposite. FULL OUTER JOIN does both.
Inserting/Updating
INSERT INTO employee VALUES(1, 'Tom', 'Developer');
INSERT INTO employee(employee_id, name) VALUES(2, 'Jim');
UPDATE employee SET role = 'Dev'
WHERE role = 'Starter';
UPDATE employee SET rate=9.70, role='Starter'
WHERE employee_id=5 OR employee_id=10;
Update without where updates all
DELETE works same as UPDATE
Functions
SELECT COUNT (employee_id) FROM employee;
SELECT COUNT (employee_id) FROM employee
WHERE rate < 10 AND name <> 'Bob';
SELECT AVG(rate) FROM employee;
SELECT COUNT(rate), rate
FROM employee
GROUP BY rate;
Also SUM
Unions
SELECT blah
UNION
SELECT blah;
Must be selecting same amount of columns.
Must have similar data type.
Nested Queries
SELECT employee.name FROM employee
WHERE employee.id IN (
    SELECT branch.mgr_id FROM branch
);
Triggers
DELIMITER $$
CREATE
    TRIGGER raise BEFORE INSERT
    ON manager
    FOR EACH ROW BEGIN
         UPDATE employee SET rate=100
         WHERE employee.id = NEW.id;
    END$$
DELIMITER ;
Can use IF THEN ELSEIF THEN ELSE END IF;
BEFORE/AFTER
DROP TRIGGER
