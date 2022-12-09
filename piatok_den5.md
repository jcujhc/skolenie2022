##  PRIPRAVA
prihlaste sa do vlastnej databazy mozte aj ako sysdba a vytvorte tabulku futbalisti <br />

create table futbalisti <br />
(id number, <br />
meno varchar2(20),  <br />
priezvisko varchar2(30),  <br />
plat number, <br />
inserted date <br />
); <br />

insert into futbalisti values (1, 'Jozef', 'Palencar', 1000, sysdate); <br />
insert into futbalisti values (2, 'Peter', 'Pekarik', 2000,sysdate); <br />
insert into futbalisti values (3, 'Ondrej', 'Duda', 3000,sysdate); <br />
insert into futbalisti values (4, 'Laco', 'Molnar', 4000,sysdate); <br />
insert into futbalisti values (5, 'Jozko', 'Kozlej', 5000,sysdate); <br />
insert into futbalisti values (6, 'Vlado', 'Zvara', 6000,sysdate); <br />
insert into futbalisti values (7, 'Pavol', 'Dina', 7000,sysdate); <br />
insert into futbalisti values (8, 'Ruslan', 'Lubarskiy',8000, sysdate); <br />


##  ULOHA
### 1.
urobte backup tabulky futbalisti (futbalisti_bck) pomocou sql prikazu  <br />
updatnite tabulku futbalisti  nastavte plat 10000 pre futbalistu s menom Laco      <br />
updatnite tabulku futbalisti  zvyste plat o 150eur pre futbalistu s id 2 a id 3.   <br />

### 2.
Otvorte si druhu session a overte svoje zmeny  <br />

### 3.
vytvorte tabulku s nazvom odpoved ktora bude mat 5 stlpcov typu varchar(20):  <br />
meno <br />
priezvisko <br />
odpoved1 <br />
odpoved2 <br />
odpoved3 <br />

### 4.
Odpovedzte na 3 otazky a odpovede zapiste do tabulky odpoved v tvare: <br />
vase meno, <br />
vase priezvisko, <br />
odpoved1 na otazku c1, <br />
odpoved2 na otazku c2, <br />
odpoved3 na otazku c3, <br />

1. Prikaz "update" patri do skupiny DML alebo DDL ? odpovedzde: DDL/DML <br />
2. Pre ktory prikaz viem dat rollback ? (drop | delete | truncate)   <br />
3. Bolo skolenie pre vas uzitocne? odpovedzde: ANO/NIE <br />


### Bonus
tabulky futbalisti a odpoved si vyexportujte  <br />














