sqlplus / as sysdba <br />

create tablespace MOJTABLESPACE datafile '/u02/data/tSKDB/mojtablespace01.dbf' size 5G; <br />

create user dbadm identified by start123 default tablespace MOJTABLESPACE; <br />




