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

commit; <br />

exit; <br />

### EXPORT DAT

expdp expdp \"/ as sysdba\" schema=testuser directory=DPDIR dumpfile=export_2testuser.dmp <br />

### IMPORT DAT

impdp \"/ as sysdba\" schema=testuser directory=DPDIR dumpfile=export_2testuser.dmp <br />


