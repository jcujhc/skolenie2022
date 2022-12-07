
## pripojenie do svojej DB ako oracle user

sqlplus / as sysdba <br />

create table t1 as select * from all_tables; <br />

create user aplikac identified by start123 default tablespace MOJTABLESPACE; <br />
grant create session to aplikac;  <br />
grant create table to aplikac;  <br /> 
alter user aplikac quota 100M on MOJTABLESPACE;  <br />

select file_name, bytes/1024/1024 MB from dba_data_files; <br />

set lines 160 <br />
col FILE_NAME for a40 <br />
SELECT FILE_NAME, TABLESPACE_NAME, STATUS FROM DBA_DATA_FILES; <br />

select username, account_status, created from dba_users where username = 'aplikac'; <br />

set lines 160 <br />
col USERNAME for a10 <br />
select username, account_status, created from dba_users where username = 'APLIKAC'; <br />

select username, account_status, created from dba_users where username like 'A%'; <br />

alter user APLIKAC account lock;  <br />

select username, account_status, created, default_tablespace from dba_users where username = 'APLIKAC'; <br />

alter user APLIKAC account unlock;  <br />

conn APLIKAC/start123 <br />

create table dev1_t1 (id int, name varchar2(20)); <br />
insert into dev1_t1 values (1,'Lala'); <br />
insert into dev1_t1 values (2,'Lala'); <br />
insert into dev1_t1 values (3,'Lala'); <br />
insert into dev1_t1 values (4,'Lala'); <br />
insert into dev1_t1 values (5,'Lala'); <br />
commit; <br />


spool /tmp/log.txt  <br />
select * from dev1_t1 ; <br />
spool off; <br />

!cat /tmp/log.txt <br />


## check size of table

conn sys as sysdba   -- opyta password <br />
Enter password: <br />


select segment_name,segment_type, sum(bytes/1024/1024) MB <br />
 from dba_segments <br />
 where segment_name='&Your_Table_Name'  <br />
group by segment_name,segment_type;  <br />


## check size tablespace

SELECT SUM(bytes/1024/1024/1024) "Size in GB" from DBA_DATA_FILES WHERE TABLESPACE_NAME='MOJTABLESPACE'; <br />

SELECT ROUND( SUM(Q1."Data Files" + Q2."Temp Files" + Q3."Redo Logs" + Q4."Control Files" )/1024/1024/1024, 2) AS "Total Size (GB)"  <br />
FROM (SELECT SUM(bytes) "Data Files" from DBA_DATA_FILES) Q1, (SELECT SUM(bytes) "Temp Files" from DBA_TEMP_FILES) Q2,  <br />
(SELECT SUM(bytes) "Redo Logs" from V_$LOG) Q3, (SELECT SUM(BLOCK_SIZE * FILE_SIZE_BLKS)"Control Files" FROM V$CONTROLFILE) Q4; <br />

## check instance

SELECT INSTANCE_NAME, HOST_NAME, VERSION, STARTUP_TIME, STATUS FROM V$INSTANCE;


