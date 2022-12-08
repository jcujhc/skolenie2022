## cviko2

### nahlasit sa as sysdba
sqlplus / as sysdba <br />

### vytvorit noveho usera 
create user testuser identified by start123 default tablespace MOJTABLESPACE; <br />
grant create session to testuser; <br />
grant create table to testuser; <br />
alter user testuser quota 100M on MOJTABLESPACE; <br />
grant read,write on directory DPDIR to testuser; <br />

### insert dat

conn testuser/start123 <br />

CREATE TABLE oddelenia <br /> 
( dept_id int NOT NULL, <br />
dept_name varchar2(50) NOT NULL, <br />
dept_headof varchar2(50) NOT NULL, <br />
CONSTRAINT departments_pk PRIMARY KEY (dept_id) <br />
); <br />

CREATE TABLE zamestnanci <br />
( emp_number int NOT NULL, <br />
last_name varchar2(50) NOT NULL, <br />
first_name varchar2(50) NOT NULL, <br />
salary number, <br />
dept_id number, <br />
CONSTRAINT employees_pk PRIMARY KEY (emp_number) <br />
); <br />

INSERT INTO oddelenia (dept_id, dept_name, dept_headof) VALUES (4567, 'GSO SAP 5','Verner, Igor'); <br />
INSERT INTO oddelenia (dept_id, dept_name, dept_headof) VALUES (1267, 'TSO AM 4','Lycka-Kubalakova, Marcela'); <br />
INSERT INTO oddelenia (dept_id, dept_name, dept_headof) VALUES (7659, 'LIM','Kasper, Kornelis'); <br />
INSERT INTO oddelenia (dept_id, dept_name, dept_headof) VALUES (9217, 'EMEA GBOLIM','Tokarova, Andrea'); <br />

INSERT INTO zamestnanci (emp_number, last_name, first_name, salary, dept_id) VALUES (460061, 'Molnar', 'Ivan', 700, 4567);
INSERT INTO zamestnanci (emp_number, last_name, first_name, salary, dept_id) VALUES (329099, 'Molnar', 'Jozef', 820, 7659);
INSERT INTO zamestnanci (emp_number, last_name, first_name, salary, dept_id) VALUES (534001, 'Beck', 'Samoel', 900, 9217);
INSERT INTO zamestnanci (emp_number, last_name, first_name, salary, dept_id) VALUES (261942, 'Liba', 'Daniel', 650, 9217);
INSERT INTO zamestnanci (emp_number, last_name, first_name, salary, dept_id) VALUES (209818, 'Vancakova', 'Ivana', 1200, 1267);

commit; <br />

exit; <br />

### EXPORT DAT

expdp / as sysdba schemas=testuser directory=DPDIR dumpfile=export_2testuser.dmp <br />
fsd

### IMPORT DAT

impdp / as sysdba schemas=testuser directory=DPDIR dumpfile=export_2testuser.dmp <br />


