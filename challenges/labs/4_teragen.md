# HDFS test

Full teragen command: 
```
[kang@london tmp]$ time hadoop jar /opt/cloudera/parcels/CDH/jars/hadoop-examples.jar teragen -D dfs.blocksize=16777216 -D mapred.map.tasks=8 51200000 /user/kang/tgen512m
```

Output of time command: 
```
real    1m9.633s
user    0m4.900s
sys     0m0.313s
```

Checking what did so far:
```
[kang@london tmp]$ hdfs dfs -ls /user/kang/tgen512m
Found 9 items
-rw-r--r--   3 kang supergroup          0 2018-03-15 14:39 /user/kang/tgen512m/_SUCCESS
-rw-r--r--   3 kang supergroup  640000000 2018-03-15 14:38 /user/kang/tgen512m/part-m-00000
-rw-r--r--   3 kang supergroup  640000000 2018-03-15 14:38 /user/kang/tgen512m/part-m-00001
-rw-r--r--   3 kang supergroup  640000000 2018-03-15 14:38 /user/kang/tgen512m/part-m-00002
-rw-r--r--   3 kang supergroup  640000000 2018-03-15 14:38 /user/kang/tgen512m/part-m-00003
-rw-r--r--   3 kang supergroup  640000000 2018-03-15 14:38 /user/kang/tgen512m/part-m-00004
-rw-r--r--   3 kang supergroup  640000000 2018-03-15 14:39 /user/kang/tgen512m/part-m-00005
-rw-r--r--   3 kang supergroup  640000000 2018-03-15 14:39 /user/kang/tgen512m/part-m-00006
-rw-r--r--   3 kang supergroup  640000000 2018-03-15 14:39 /user/kang/tgen512m/part-m-00007
```

Blocks linked to the directory: 
```
[kang@london tmp]$ hadoop fsck /user/kang/tgen512m
DEPRECATED: Use of this script to execute hdfs command is deprecated.
Instead use the hdfs command for it.

Connecting to namenode via http://amsterdam.c.sebc-challenges-198020.internal:50070
FSCK started by kang (auth:SIMPLE) from /10.142.0.5 for path /user/kang/tgen512m at Thu Mar 15 14:40:29 UTC 2018
.........Status: HEALTHY
 Total size:    5120000000 B
 Total dirs:    1
 Total files:   9
 Total symlinks:                0
 Total blocks (validated):      312 (avg. block size 16410256 B)
 Minimally replicated blocks:   312 (100.0 %)
 Over-replicated blocks:        0 (0.0 %)
 Under-replicated blocks:       0 (0.0 %)
 Mis-replicated blocks:         0 (0.0 %)
 Default replication factor:    3
 Average block replication:     3.0
 Corrupt blocks:                0
 Missing replicas:              0 (0.0 %)
 Number of data-nodes:          3
 Number of racks:               1
FSCK ended at Thu Mar 15 14:40:29 UTC 2018 in 12 milliseconds


The filesystem under path '/user/kang/tgen512m' is HEALTHY
```