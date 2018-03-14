# Sentry 

## Before 
```
[root@berlin tmp]# kinit sebc
Password for sebc@HADOOP.COM:
[root@berlin tmp]# clear
[root@berlin tmp]# beeline
Beeline version 1.1.0-cdh5.9.3 by Apache Hive
beeline> !connect jdbc:hive2://localhost:10000/default;principal=hive/berlin.c.sebc-labs.internal@HADOOP.COM
scan complete in 2ms
Connecting to jdbc:hive2://localhost:10000/default;principal=hive/berlin.c.sebc-labs.internal@HADOOP.COM
Connected to: Apache Hive (version 1.1.0-cdh5.9.3)
Driver: Hive JDBC (version 1.1.0-cdh5.9.3)
Transaction isolation: TRANSACTION_REPEATABLE_READ
0: jdbc:hive2://localhost:10000/default> SHOW TABLES;
INFO  : Compiling command(queryId=hive_20180314165757_87aad96d-9430-4b1d-94a2-39dbfd5bf324): SHOW TABLES
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:[FieldSchema(name:tab_name, type:string, comment:from deserializer)], properties:null)
INFO  : Completed compiling command(queryId=hive_20180314165757_87aad96d-9430-4b1d-94a2-39dbfd5bf324); Time taken: 0.664 seconds
INFO  : Executing command(queryId=hive_20180314165757_87aad96d-9430-4b1d-94a2-39dbfd5bf324): SHOW TABLES
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20180314165757_87aad96d-9430-4b1d-94a2-39dbfd5bf324); Time taken: 0.351 seconds
INFO  : OK
+-----------+--+
| tab_name  |
+-----------+--+
+-----------+--+
No rows selected (1.408 seconds)
0: jdbc:hive2://localhost:10000/default>
```

## After 
```
jdbc:hive2://localhost:10000/default> GRANT ROLE sentry_admin TO GROUP hive;
INFO  : Compiling command(queryId=hive_20180314170808_470bc120-2511-4859-81d8-c773bafe9cac): GRANT ROLE sentry_admin TO GROUP hive
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:null, properties:null)
INFO  : Completed compiling command(queryId=hive_20180314170808_470bc120-2511-4859-81d8-c773bafe9cac); Time taken: 0.064 seconds
INFO  : Executing command(queryId=hive_20180314170808_470bc120-2511-4859-81d8-c773bafe9cac): GRANT ROLE sentry_admin TO GROUP hive
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20180314170808_470bc120-2511-4859-81d8-c773bafe9cac); Time taken: 0.148 seconds
INFO  : OK
No rows affected (0.23 seconds)
0: jdbc:hive2://localhost:10000/default> SHOW TABLES;
INFO  : Compiling command(queryId=hive_20180314170808_a65bcbe0-80c4-466f-8548-23e292aa40c9): SHOW TABLES
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:[FieldSchema(name:tab_name, type:string, comment:from deserializer)], properties:null)
INFO  : Completed compiling command(queryId=hive_20180314170808_a65bcbe0-80c4-466f-8548-23e292aa40c9); Time taken: 0.075 seconds
INFO  : Executing command(queryId=hive_20180314170808_a65bcbe0-80c4-466f-8548-23e292aa40c9): SHOW TABLES
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20180314170808_a65bcbe0-80c4-466f-8548-23e292aa40c9); Time taken: 0.166 seconds
INFO  : OK
+------------+--+
|  tab_name  |
+------------+--+
| customers  |
| mock_data  |
| sample_07  |
| sample_08  |
| web_logs   |
+------------+--+
5 rows selected (0.313 seconds)
```

George should be able to read all the tables (indeed he can): 
```
[root@berlin tmp]# kinit george
Password for george@HADOOP.COM:
[root@berlin tmp]# beeline
Beeline version 1.1.0-cdh5.9.3 by Apache Hive
beeline> SHOW TABLES;
No current connection
beeline> !connect jdbc:hive2://localhost:10000/default;principal=hive/berlin.c.sebc-labs.internal@HADOOP.COM
scan complete in 2ms
Connecting to jdbc:hive2://localhost:10000/default;principal=hive/berlin.c.sebc-labs.internal@HADOOP.COM
Connected to: Apache Hive (version 1.1.0-cdh5.9.3)
Driver: Hive JDBC (version 1.1.0-cdh5.9.3)
Transaction isolation: TRANSACTION_REPEATABLE_READ
0: jdbc:hive2://localhost:10000/default> SHOW TABLES;
INFO  : Compiling command(queryId=hive_20180314171616_12d43dbc-bbe4-4212-862c-e4cb853088a4): SHOW TABLES
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:[FieldSchema(name:tab_name, type:string, comment:from deserializer)], properties:null)
INFO  : Completed compiling command(queryId=hive_20180314171616_12d43dbc-bbe4-4212-862c-e4cb853088a4); Time taken: 0.112 seconds
INFO  : Executing command(queryId=hive_20180314171616_12d43dbc-bbe4-4212-862c-e4cb853088a4): SHOW TABLES
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20180314171616_12d43dbc-bbe4-4212-862c-e4cb853088a4); Time taken: 0.178 seconds
INFO  : OK
+------------+--+
|  tab_name  |
+------------+--+
| customers  |
| mock_data  |
| sample_07  |
| sample_08  |
| web_logs   |
+------------+--+
5 rows selected (0.394 seconds)
```

Ferdinand, instead, is able to see only __mock_data__ table:
```
[root@berlin tmp]# kinit ferdinand
Password for ferdinand@HADOOP.COM:
[root@berlin tmp]# beeline
Beeline version 1.1.0-cdh5.9.3 by Apache Hive
beeline> !connect jdbc:hive2://localhost:10000/default;principal=hive/berlin.c.sebc-labs.internal@HADOOP.COM
scan complete in 2ms
Connecting to jdbc:hive2://localhost:10000/default;principal=hive/berlin.c.sebc-labs.internal@HADOOP.COM
Connected to: Apache Hive (version 1.1.0-cdh5.9.3)
Driver: Hive JDBC (version 1.1.0-cdh5.9.3)
Transaction isolation: TRANSACTION_REPEATABLE_READ
0: jdbc:hive2://localhost:10000/default> SHOW TABLES;
INFO  : Compiling command(queryId=hive_20180314171818_6b381c06-8d67-4584-b7a7-97d986025c9f): SHOW TABLES
INFO  : Semantic Analysis Completed
INFO  : Returning Hive schema: Schema(fieldSchemas:[FieldSchema(name:tab_name, type:string, comment:from deserializer)], properties:null)
INFO  : Completed compiling command(queryId=hive_20180314171818_6b381c06-8d67-4584-b7a7-97d986025c9f); Time taken: 0.077 seconds
INFO  : Executing command(queryId=hive_20180314171818_6b381c06-8d67-4584-b7a7-97d986025c9f): SHOW TABLES
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20180314171818_6b381c06-8d67-4584-b7a7-97d986025c9f); Time taken: 0.145 seconds
INFO  : OK
+------------+--+
|  tab_name  |
+------------+--+
| mock_data  |
+------------+--+
1 row selected (0.334 seconds)
```
