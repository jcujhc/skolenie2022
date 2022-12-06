## CREATE TABLE STATEMENT

CREATE TABLE oddelenia
( dept_id int NOT NULL,
  dept_name char(50) NOT NULL,
  dept_headof char(50) NOT NULL,
  CONSTRAINT departments_pk PRIMARY KEY (dept_id)
);

INSERT INTO oddelenia (dept_id, dept_name, dept_headof) VALUES (4567, 'GSO SAP 5','Verner, Igor'); <br />
INSERT INTO oddelenia (dept_id, dept_name, dept_headof) VALUES (1267, 'TSO AM 4','Lycka-Kubalakova, Marcela'); <br />
INSERT INTO oddelenia VALUES (7659, 'LIM','Kasper, Kornelis'); <br />
INSERT INTO oddelenia (dept_id, dept_name) VALUES (9217, 'EMEA GBO & LIM','Tokarova, Andrea'); <br />

select * from oddelenia; <br />

select dept_id,last_name,first_name from zamestnanci where last_name = '%ova'; <br />

select LAST_NAME,FIRST_NAME,SALARY from zamestnanci order by SALARY; <br />


## INSERT STATEMENT - slúži pre vkladanie dát

CREATE TABLE zamestnanci
( emp_number int NOT NULL,
  last_name char(50) NOT NULL,
  first_name char(50) NOT NULL,
  salary number,
  dept_id number,
  CONSTRAINT employees_pk PRIMARY KEY (emp_number)
);

insert into zamestnanci values (23456,' Kasper','Jozef',NULL,262613); <br />
insert into zamestnanci(id,priezvisko,meno) values (23456,' Kasper ','Jozef'); <br />


## UPDATE STATEMENT - slúži pre zmenu dát

update zamestnanci set SALARY = SALARY + 100; <br />


## DELETE / TRUNCATE STATEMENT - slúži na mazanie dát
DELETE - mazanie dát s podmienkou  <br />
       - neuvoľní priestor v TBS, vytvára archívny záznam <br />

delete from zamestnanci where LAST_NAME = 'Kasper'; <br />

## TRUNCATE - mazanie dát bez podmienky
- uvoľní priestor v TBS,nevytvára archívny záznam, nenávratná oper <br />

truncate table zamestnanci; <br />



# EXPDP / IMPDP

mkdir /u02/data/export <br />
create or replace directory DPDIR as '/u02/data/export'; <br />
grant read,write on DPDIR to appadm; <br />

### EXPDP
$ expdp appadm/start123 schemas=appadm directory=DPDIR dumpfile=export_appadm.dmp <br />

### IMPDP
$ impdp appadm/start123@SKOLENIE schemas=appadm directory=DPDIR dumpfile=export.dmp <br />


### EXPDP/IMPDP použitím par file
file: mojexport.par v
USERID=student01/start123 <br />
DIRECTORY=DPDIR <br />
DUMPFILE=expdp_db.30072019.dmp <br />
LOGFILE=expdp_db.30072019.log <br />
SCHEMAS=student1 <br />

-- or TABLES=EMPLOYEES, DEPARTMENTS <br />

$ expdp parfile=mojexport.par <br />


### MOŽNOSTI IMPDP

table_exists_action je použitá pri impdp keď tabuľka už existuje v DB  <br />
                 
table_exists_action=skip:  ignoruj data v import file a nechaj existujúcu tabuľku nedotknutú. Toto je default option a neplatí pri nastavení  content=data_only. <br />

table_exists_action=append:  týmto sa povie, pridaj exportované dá do existujúcej tabuľky, nechaj exist. riadny a pridaj nové. <br />

table_exists_action=truncate:  toto nám vraví, truncate existujúcu tabuľku, ponechaj štruktúru a importni riadky z dump file. Pri použití tejto option nesmie existovat  referenčné integrita (constraints) na cieľovej tabuľke.  <br />

