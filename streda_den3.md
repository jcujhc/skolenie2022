
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

@/tmp/einstein.txt

### select

select * from einstein;

### create backup table

create table einstein_bck as select * from einstein;

### insert new data


### update table


### delete from












