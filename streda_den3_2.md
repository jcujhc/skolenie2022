## SESSION1
sqlplus user05/start123@//10.233.133.153:1521/tSKDB <br />

sqlplus userXX/start123@//10.233.133.XXX:1521/SKOLENIE <br />

## SESSION2
set lines 160 <br />
col username for a15 <br />

select USERNAME, SID, SERIAL#, PROGRAM, LOGON_TIME from v$session;  <br />

select USERNAME, SID, SERIAL#, PROGRAM, LOGON_TIME from v$session where USERNAME is not null;  <br />


# DEMO EXPORT

## SESSION applikac

sqlplus aplikac/start123@DB_SKOLENIE <br />

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


INSERT INTO zamestnanci (emp_number, last_name, first_name, salary, dept_id) VALUES (460061, 'Molnar', 'Ivan', 700, 4567); <br />
INSERT INTO zamestnanci (emp_number, last_name, first_name, salary, dept_id) VALUES (329099, 'Molnar', 'Jozef', 820, 7659); <br />
INSERT INTO zamestnanci (emp_number, last_name, first_name, salary, dept_id) VALUES (534001, 'Beck', 'Samoel', 900, 9217); <br />
INSERT INTO zamestnanci (emp_number, last_name, first_name, salary, dept_id) VALUES (261942, 'Liba', 'Daniel', 650, 9217); <br />
INSERT INTO zamestnanci (emp_number, last_name, first_name, salary, dept_id) VALUES (209818, 'Vancakova', 'Ivana', 1200, 1267); <br />

commit; <br />

exit; <br />


AS ORACLE <br />
mkdir /u02/data/export <br />

sqlplus / as sysdba <br />
-- resp <br />
sqlplus /nolog  <br />
conn sys as sysdba <br />
create or replace directory DPDIR as '/u02/data/export'; <br />
grant read,write on directory  DPDIR to aplikac; <br />

## EXPDP
$ expdp aplikac/start123@DB_SKOLENIE schemas=aplikac directory=DPDIR dumpfile=export_aplikac.dmp <br />

## IMPDP
$ impdp aplikac/start123@DB_SKOLENIE schemas=aplikac directory=DPDIR dumpfile=export_aplikac.dmp <br />

## EXPDP/IMPDP použitím par file 
-- file: mojexport.par  <br />
USERID=aplikac/start123@DB_SKOLENIE <br />
DIRECTORY=DPDIR <br />
DUMPFILE=export_aplikac.dmp <br />
LOGFILE=impdp_db.30072019.log <br />
SCHEMAS=aplikac <br />

-- or TABLES=EMPLOYEES, DEPARTMENTS <br />

$ expdp parfile=mojexport.par <br />

## MOŽNOSTI IMPDP 
table_exists_action je použitá pri impdp keď tabuľka už existuje v DB <br />

table_exists_action=skip: ignoruj data v import file a nechaj existujúcu tabuľku nedotknutú.  <br />
                          Toto je default option a neplatí pri nastavení content=data_only.   <br />

table_exists_action=append: týmto sa povie, pridaj exportované dá do existujúcej tabuľky, nechaj exist. riadny a pridaj nové. <br />

table_exists_action=truncate: toto nám vraví, truncate existujúcu tabuľku, ponechaj štruktúru a importni riadky z dump file.  <br />
                              Pri použití tejto option nesmie existovat referenčné integrita (constraints) na cieľovej tabuľke. <br />


$ impdp aplikac/start123@DB_SKOLENIE schemas=appadm directory=DPDIR dumpfile=export.dmp <br />
