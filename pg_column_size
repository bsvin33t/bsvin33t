My PM wanted me to find the largest and the smallest field in a table for a jsonb column.

I ended up using 

`SELECT pg_column_size(value -> 'json_column_name'), id from table;`

This worked quite well.

Cheers
Vineeth
