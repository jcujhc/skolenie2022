
### connect

sudo su - <br />
 
su - oracle <br />

sqlplus userXX/start123@//10.233.133.153:1521/tSKDB <br />

### create table

create table einstein( <br />
id number, <br />
meno varchar2(20), <br />
priezvisko varchar2(40), <br />
email varchar2(40), <br />
telefon varchar2(30), <br />
insert_date date); <br />

### run script

@/tmp/einstein.txt <br />
commit; 

### select

select * from einstein; <br />

set lines 160 <br />
col MENO for a15
col PRIEZVISKO for a15 <br />
col EMAIL for a35 <br />
select * from einstein; <br />

select * from einstein where priezvisko like '%ov%'; <br />

### create backup table

create table einstein_bck as select * from einstein;

### insert new data

INSERT INTO einstein VALUES (23570,'Fero','Lam','frantisek.lam@t-systems','+42158745692',sysdate);<br />
commit;

### update table

update einstein set meno='Frantisek' where id=23570; <br />
commit;

### delete from

delete from einstein where id=23570; <br />
commit; <br />

select * from einstein; <br />

delete from einstein where id=23570; <br />
commit; <br />


### insert data back

INSERT INTO einstein select * from einstein_bck;







