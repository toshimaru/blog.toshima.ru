---
layout: post
title: "MySQL: How to get the size of tables"
tags: mysql
---

You can get the size of tables by using `information_schema` in MySQL.

## Query

List top 10 biggest size of tables.

```sql
SELECT TABLE_NAME,
       TABLE_ROWS,
       AVG_ROW_LENGTH,
       floor((DATA_LENGTH) / 1024 / 1024) AS 'DATA_LENGTH(MB)',
       floor((INDEX_LENGTH) / 1024 / 1024) AS 'INDEX_LENGTH(MB)',
       floor((DATA_LENGTH + INDEX_LENGTH) / 1024 / 1024) AS 'ALL_DATA_LENGTH(MB)'
FROM information_schema.tables
WHERE table_schema=database()
ORDER BY (DATA_LENGTH + INDEX_LENGTH) DESC
LIMIT 10;
```

| column | description |
| --- | --- |
| `TABLE_NAME`  | table name  |
| `TABLE_ROWS`  | table rows count  |
| `AVG_ROW_LENGTH`  | average row data length  |
| `DATA_LENGTH`  | table data length  |
| `INDEX_LENGTH`  | table index data length  |
| `ALL_DATA_LENGTH`  | table data + index data length  |
