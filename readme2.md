## CREATE TABLE STATEMENT

CREATE TABLE oddelenia
( dept_id int NOT NULL,
  dept_name char(50) NOT NULL,
  dept_headof char(50) NOT NULL,
  CONSTRAINT departments_pk PRIMARY KEY (dept_id)
);

INSERT INTO oddelenia (dept_id, dept_name, dept_headof) VALUES (4567, 'GSO SAP 5','Verner, Igor');
INSERT INTO oddelenia (dept_id, dept_name, dept_headof) VALUES (1267, 'TSO AM 4','Lycka-Kubalakova, Marcela');
INSERT INTO oddelenia VALUES (7659, 'LIM','Kasper, Kornelis');
INSERT INTO oddelenia (dept_id, dept_name) VALUES (9217, 'EMEA GBO & LIM','Tokarova, Andrea');

select * from oddelenia;
select dept_id,last_name,first_name from zamestnanci where last_name = '%ova';
select LAST_NAME,FIRST_NAME,SALARY from zamestnanci order by SALARY;


INSERT STATEMENT - slúži pre vkladanie dát
insert into zamestnanci values (23456,' Kasper','Jozef',NULL,262613);
insert into zamestnanci(id,priezvisko,meno) 
       values (23456,' Kasper ','Jozef');

UPDATE STATEMENT - slúži pre zmenu dát
update zamestnanci set SALARY = SALARY + 100;


DELETE / TRUNCATE STATEMENT - slúži na mazanie dát
DELETE - mazanie dát s podmienkou 
       - neuvoľní priestor v TBS, vytvára archívny záznam

TRUNCATE - mazanie dát bez podmienky
         - uvoľní priestor v TBS,nevytvára archívny záznam, nenávratná oper.
delete from zamestnanci where LAST_NAME = 'Kasper';

truncate table zamestnanci;


