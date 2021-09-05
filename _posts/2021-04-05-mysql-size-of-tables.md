---
layout: post
title: "MySQL: How to get the size of tables"
tags: mysql
last_modified_at: 2021-09-05
---

You can get the size of tables by using `information_schema` in MySQL.

## Query

List top 10 biggest size of tables.

```sql
SELECT table_schema,
       table_name,
       table_rows,
       avg_row_length,
       floor((data_length + index_length + data_free)/1024/1024) AS 'total(mb)',
       floor((data_length)/1024/1024) AS 'data(mb)',
       floor((index_length)/1024/1024) AS 'index(mb)',
       floor((data_free)/1024/1024) AS 'free(mb)'
FROM information_schema.tables
WHERE table_schema=database()
ORDER BY 5 DESC
limit 10;
```

| column | description |
| --- | --- |
| `table_name`  | table name  |
| `table_rows`  | table rows count  |
| `avg_row_length`  | average row data length  |
| `data_length`  | table data length  |
| `index_length`  | table index data length  |
| `all_data_length`  | table data + index data length  |

## Reference

- [Optimize disk storage when Amazon RDS for MySQL uses more storage than expected](https://aws.amazon.com/premiumsupport/knowledge-center/rds-mysql-storage-optimization/?nc1=h_ls)
