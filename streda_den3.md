
### connect

sudo su - <br />
 
su - oracle <br />

sqlplus userXX/start123@//10.233.133.153:1521/tSKDB <br />

vyskusat <br />
sqlplus userXX/start123@DB_tSKDB <br />


### create table

create table einstein( <br />
id number, <br />
meno varchar2(20), <br />
priezvisko varchar2(40), <br />
email varchar2(40), <br />
telefon varchar2(30), <br />
insert_date date); <br />

select table_name from user_tables; <br />

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

delete from einstein; <br />
rollback; <br />

truncate table einstein; <br />
rollback; <br />

select * from einstein; <br />

### insert data back

INSERT INTO einstein select * from einstein_bck; <br />
commit; <br />

drop table einstein; <br />
rollback; <br />

select * from einstein; <br />

desc einstein <br />

create table einstein as select * from einstein_bck; <br />

create table einstein as select id,meno,priezvisko from einstein_bck; <br />







