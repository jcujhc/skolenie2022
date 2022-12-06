# skolenie2022

## connection

create user appadm identified by 'start123'; <br />

sqlplus appadm/start123@//10.233.133.153:1521 <br />

sqlplus appadm/start123@'(DESCRIPTION=(ADDRESS_LIST=(ADDRESS=(PROTOCOL=TCP)(HOST=10.233.133.153:1521)(PORT=1521))(CONNECT_DATA=(SID=tSKDB)(SERVER=DEDICATED)))' 
<br />

show user; <br />

grant create session to appadm; <br />
grant create table to appadm; <br />
alter user appadm quota 100M on USERS;


### Managing Users and Security
## 1. List all users, account status and profile
   SELECT USERNAME, ACCOUNT_STATUS, PROFILE FROM DBA_USERS;
   
## 2. List all roles
   SELECT * FROM DBA_ROLES;
   
## 3. Create User
   CREATE USER charlie IDENTIFIED BY password123;
   Note: Two administrative user accounts SYS and SYSTEM are created by default. Default password for SYS user is CHANGE_ON_INSTALL and SYSTEM user is MANAGER
   
## 4. Change user password
   ALTER USER charlie IDENTIFIED BY newpassword;
    - or -
   PASSWORD
   
## 5. Create user profile (with all default limits)
   CREATE PROFILE MY_PROFILE LIMIT;
   
## 6. View all user profiles and limits
   SELECT * FROM DBA_PROFILES;
   SELECT * FROM DBA_PROFILES WHERE PROFILE='MY_PROFILE';
   
## 7. Change password lifetime, reuse time, failed login attempts
   SELECT * FROM DBA_PROFILES WHERE PROFILE='MY_PROFILE' AND RESOURCE_NAME = 'PASSWORD_LIFE_TIME';
   
## 8. Set password expiry
To set password to 60 days for example:

   ALTER PROFILE MY_NEW_PROFILE LIMIT PASSWORD_LIFE_TIME 60;
To set password to never expire:

   ALTER PROFILE MY_PROFILE LIMIT PASSWORD_LIFE_TIME UNLIMITED;
## 9. View privileges granted to a user on other users tables
   SELECT * FROM DBA_TAB_PRIVS WHERE GRANTEE='USERNAME';
## 10. View all user privileges including the privileges that are indirectly granted through roles
   SELECT * FROM DBA_SYS_PRIVS WHERE GRANTEE='USERNAME' or GRANTEE in (SELECT GRANTED_ROLE FROM DBA_ROLE_PRIVS WHERE GRANTEE='USERNAME');



### 1. View the version of Oracle that is installed.
   SELECT * FROM PRODUCT_COMPONENT_VERSION; <br />
    - or - <br />
   SELECT * FROM V$VERSION; <br />
   
### 2. View database name.
   SELECT NAME FROM V$DATABASE; <br />
    - or - <br />
   SELECT * FROM GLOBAL_NAME; <br />
### 3. View NLS (National Language Support) Parameters
   SELECT * FROM NLS_DATABASE_PARAMETERS; <br />
    - or - <br />
   SELECT * FROM V$NLS_PARAMETERS; <br />
   
### 4. View Sessions
   SELECT SCHEMANAME, OSUSER, MACHINE, PROGRAM, STATE FROM V$SESSION; <br />
   
### 5. View Services
   SELECT SERVICE_ID, NAME, NETWORK_NAME FROM DBA_SERVICES; <br />
   
### 6. View current database instance details
   SELECT INSTANCE_NAME, HOST_NAME, VERSION, STARTUP_TIME, STATUS FROM V$INSTANCE; <br />

## Managing Tablespaces and Data files
### 1. List tablespaces, status and type
   SELECT TABLESPACE_NAME, STATUS, CONTENTS FROM DBA_TABLESPACES; <br />
   
### 2. Create tablespace
   CREATE TABLESPACE myspace 
       DATAFILE 'datafile_directory_path\data_file_name.dbf' 
       SIZE 20M 
       AUTOEXTEND ON
       NEXT 512K
    MAXSIZE UNLIMITED;
    
### 3. List Datafiles, tablespaces and status
   SELECT FILE_NAME, TABLESPACE_NAME, STATUS FROM DBA_DATA_FILES;
   
### 4. To check the current size of a tablespace
   SELECT SUM(bytes/1024/1024/1024) "Size in GB" from DBA_DATA_FILES WHERE TABLESPACE_NAME='MYSPACE';

## List Datafiles, tablespaces and status
   SELECT FILE_NAME, TABLESPACE_NAME, STATUS FROM DBA_DATA_FILES;

### Check the size of a database
Size of an Oracle database is the sum of the size of its Data files, Temporary files, Redo logs and Control files.

   SELECT ROUND(
       SUM(Q1."Data Files" + 
           Q2."Temp Files" + 
           Q3."Redo Logs" + 
           Q4."Control Files"
           )/1024/1024/1024,  2) 
       AS "Total Size (GB)"
   FROM
    (SELECT SUM(bytes) "Data Files" from DBA_DATA_FILES) Q1,
    (SELECT SUM(bytes) "Temp Files" from DBA_TEMP_FILES) Q2,
    (SELECT SUM(bytes) "Redo Logs" from V_$LOG) Q3,
    (SELECT SUM(BLOCK_SIZE * FILE_SIZE_BLKS)"Control Files" FROM V$CONTROLFILE) Q4;


