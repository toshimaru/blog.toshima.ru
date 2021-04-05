---
layout: post
title: "MySQL: How to get the size of tables"
tags: mysql
---

```sql
SELECT TABLE_NAME,
       TABLE_ROWS,
       AVG_ROW_LENGTH,
       floor((DATA_LENGTH + INDEX_LENGTH) / 1024 / 1024) AS 'ALL_DATA_LENGTH(MB)',
       floor((DATA_LENGTH) / 1024 / 1024) AS 'DATA_LENGTH(MB)',
       floor((INDEX_LENGTH) / 1024 / 1024) AS 'INDEX_LENGTH(MB)'
FROM information_schema.tables
WHERE table_schema=database()
ORDER BY (DATA_LENGTH + INDEX_LENGTH) DESC
LIMIT 10;
```
