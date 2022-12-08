## cviko2

sqlplus / as sysdba

create user testuser identified by start123 default tablespace MOJTABLESPACE;
grant create session to testuser;
grant create table to testuser;
alter user testuser quota 100M on MOJTABLESPACE;
grant read,write on directory DPDIR to testuser;


CREATE TABLE oddelenia
( dept_id int NOT NULL,
dept_name varchar2(50) NOT NULL,
dept_headof varchar2(50) NOT NULL,
CONSTRAINT departments_pk PRIMARY KEY (dept_id)
);

CREATE TABLE zamestnanci
( emp_number int NOT NULL,
last_name varchar2(50) NOT NULL,
first_name varchar2(50) NOT NULL,
salary number,
dept_id number,
CONSTRAINT employees_pk PRIMARY KEY (emp_number)
);

INSERT INTO oddelenia (dept_id, dept_name, dept_headof) VALUES (4567, 'GSO SAP 5','Verner, Igor');
INSERT INTO oddelenia (dept_id, dept_name, dept_headof) VALUES (1267, 'TSO AM 4','Lycka-Kubalakova, Marcela');
INSERT INTO oddelenia (dept_id, dept_name, dept_headof) VALUES (7659, 'LIM','Kasper, Kornelis');
INSERT INTO oddelenia (dept_id, dept_name, dept_headof) VALUES (9217, 'EMEA GBOLIM','Tokarova, Andrea');

commit;



expdp expdp \"/ as sysdba\" schema=testuser directory=DPDIR dumpfile=export_2testuser.dmp <br />


expdp aplikac/start123@DB_tSKDB tables=aplikac.zamestnanci directory=DPDIR dumpfile=export_aplikac_zamestnanci.dmp <br />

