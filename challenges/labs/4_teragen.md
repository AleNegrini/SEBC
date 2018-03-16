## Teragen

Teragen command: 
```
[hilary@london root]$ hdfs dfs -rm -r /user/hilary/tgen
18/03/16 10:06:13 INFO fs.TrashPolicyDefault: Moved: 'hdfs://amsterdam.c.sebc-pre-challenges.internal:8020/user/hilary/tgen' to trash at: hdfs://amsterdam.c.sebc-pre-challenges.internal:8020/user/hilary/.Trash/Current/user/hilary/tgen
[hilary@london root]$ time hadoop jar /opt/cloudera/parcels/CDH/jars/hadoop-examples.jar teragen -D dfs.blocksize=67108864 -D mapred.map.tasks=16 -D mapreduce.map.memory.mb=768 65536000 /user/hilary/tgen
18/03/16 10:06:30 INFO client.RMProxy: Connecting to ResourceManager at berlin.c.sebc-pre-challenges.internal/10.142.0.6:8032
18/03/16 10:06:30 INFO terasort.TeraGen: Generating 65536000 using 16
18/03/16 10:06:30 INFO mapreduce.JobSubmitter: number of splits:16
18/03/16 10:06:30 INFO Configuration.deprecation: mapred.map.tasks is deprecated. Instead, use mapreduce.job.maps
18/03/16 10:06:31 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_1521192866282_0003
18/03/16 10:06:31 INFO impl.YarnClientImpl: Submitted application application_1521192866282_0003
18/03/16 10:06:31 INFO mapreduce.Job: The url to track the job: http://berlin.c.sebc-pre-challenges.internal:8088/proxy/application_1521192866282_0003/
18/03/16 10:06:31 INFO mapreduce.Job: Running job: job_1521192866282_0003
18/03/16 10:06:37 INFO mapreduce.Job: Job job_1521192866282_0003 running in uber mode : false
18/03/16 10:06:37 INFO mapreduce.Job:  map 0% reduce 0%
18/03/16 10:06:56 INFO mapreduce.Job:  map 6% reduce 0%
18/03/16 10:06:58 INFO mapreduce.Job:  map 19% reduce 0%
18/03/16 10:06:59 INFO mapreduce.Job:  map 25% reduce 0%
18/03/16 10:07:00 INFO mapreduce.Job:  map 31% reduce 0%
18/03/16 10:07:13 INFO mapreduce.Job:  map 37% reduce 0%
18/03/16 10:07:14 INFO mapreduce.Job:  map 38% reduce 0%
18/03/16 10:07:15 INFO mapreduce.Job:  map 44% reduce 0%
18/03/16 10:07:19 INFO mapreduce.Job:  map 50% reduce 0%
18/03/16 10:07:20 INFO mapreduce.Job:  map 56% reduce 0%
18/03/16 10:07:22 INFO mapreduce.Job:  map 62% reduce 0%
18/03/16 10:07:23 INFO mapreduce.Job:  map 63% reduce 0%
18/03/16 10:07:31 INFO mapreduce.Job:  map 69% reduce 0%
18/03/16 10:07:36 INFO mapreduce.Job:  map 74% reduce 0%
18/03/16 10:07:38 INFO mapreduce.Job:  map 75% reduce 0%
18/03/16 10:07:39 INFO mapreduce.Job:  map 81% reduce 0%
18/03/16 10:07:43 INFO mapreduce.Job:  map 87% reduce 0%
18/03/16 10:07:44 INFO mapreduce.Job:  map 94% reduce 0%
18/03/16 10:07:45 INFO mapreduce.Job:  map 100% reduce 0%
18/03/16 10:07:45 INFO mapreduce.Job: Job job_1521192866282_0003 completed successfully
18/03/16 10:07:45 INFO mapreduce.Job: Counters: 31
        File System Counters
                FILE: Number of bytes read=0
                FILE: Number of bytes written=2366102
                FILE: Number of read operations=0
                FILE: Number of large read operations=0
                FILE: Number of write operations=0
                HDFS: Number of bytes read=1368
                HDFS: Number of bytes written=6553600000
                HDFS: Number of read operations=64
                HDFS: Number of large read operations=0
                HDFS: Number of write operations=32
        Job Counters
                Launched map tasks=16
                Other local map tasks=16
                Total time spent by all maps in occupied slots (ms)=297015
                Total time spent by all reduces in occupied slots (ms)=0
                Total time spent by all map tasks (ms)=297015
                Total vcore-milliseconds taken by all map tasks=297015
                Total megabyte-milliseconds taken by all map tasks=304143360
        Map-Reduce Framework
                Map input records=65536000
                Map output records=65536000
                Input split bytes=1368
                Spilled Records=0
                Failed Shuffles=0
                Merged Map outputs=0
                GC time elapsed (ms)=4172
                CPU time spent (ms)=133990
                Physical memory (bytes) snapshot=4967055360
                Virtual memory (bytes) snapshot=21608706048
                Total committed heap usage (bytes)=5204082688
        org.apache.hadoop.examples.terasort.TeraGen$Counters
                CHECKSUM=140750829423462787
        File Input Format Counters
                Bytes Read=0
        File Output Format Counters
                Bytes Written=6553600000
```

Output of `time` command:  
```
real    1m18.527s
user    0m5.583s
sys     0m0.314s
```

Listing the output files produced:
```
[hilary@london root]$ hdfs dfs -ls /user/hilary/tgen
Found 17 items
-rw-r--r--   3 hilary supergroup          0 2018-03-16 10:07 /user/hilary/tgen/_SUCCESS
-rw-r--r--   3 hilary supergroup  409600000 2018-03-16 10:06 /user/hilary/tgen/part-m-00000
-rw-r--r--   3 hilary supergroup  409600000 2018-03-16 10:06 /user/hilary/tgen/part-m-00001
-rw-r--r--   3 hilary supergroup  409600000 2018-03-16 10:06 /user/hilary/tgen/part-m-00002
-rw-r--r--   3 hilary supergroup  409600000 2018-03-16 10:06 /user/hilary/tgen/part-m-00003
-rw-r--r--   3 hilary supergroup  409600000 2018-03-16 10:06 /user/hilary/tgen/part-m-00004
-rw-r--r--   3 hilary supergroup  409600000 2018-03-16 10:07 /user/hilary/tgen/part-m-00005
-rw-r--r--   3 hilary supergroup  409600000 2018-03-16 10:07 /user/hilary/tgen/part-m-00006
-rw-r--r--   3 hilary supergroup  409600000 2018-03-16 10:07 /user/hilary/tgen/part-m-00007
-rw-r--r--   3 hilary supergroup  409600000 2018-03-16 10:07 /user/hilary/tgen/part-m-00008
-rw-r--r--   3 hilary supergroup  409600000 2018-03-16 10:07 /user/hilary/tgen/part-m-00009
-rw-r--r--   3 hilary supergroup  409600000 2018-03-16 10:07 /user/hilary/tgen/part-m-00010
-rw-r--r--   3 hilary supergroup  409600000 2018-03-16 10:07 /user/hilary/tgen/part-m-00011
-rw-r--r--   3 hilary supergroup  409600000 2018-03-16 10:07 /user/hilary/tgen/part-m-00012
-rw-r--r--   3 hilary supergroup  409600000 2018-03-16 10:07 /user/hilary/tgen/part-m-00013
-rw-r--r--   3 hilary supergroup  409600000 2018-03-16 10:07 /user/hilary/tgen/part-m-00014
-rw-r--r--   3 hilary supergroup  409600000 2018-03-16 10:07 /user/hilary/tgen/part-m-00015
```

Blocks associated to that folder:
```
[hilary@london root]$ hadoop fsck -blocks /user/hilary
DEPRECATED: Use of this script to execute hdfs command is deprecated.
Instead use the hdfs command for it.

Connecting to namenode via http://amsterdam.c.sebc-pre-challenges.internal:50070/fsck?ugi=hilary&blocks=1&path=%2Fuser%2Fhilary
FSCK started by hilary (auth:SIMPLE) from /10.142.0.5 for path /user/hilary at Fri Mar 16 10:09:19 UTC 2018
..................................Status: HEALTHY
 Total size:    13107200000 B
 Total dirs:    12
 Total files:   34
 Total symlinks:                0
 Total blocks (validated):      224 (avg. block size 58514285 B)
 Minimally replicated blocks:   224 (100.0 %)
 Over-replicated blocks:        0 (0.0 %)
 Under-replicated blocks:       0 (0.0 %)
 Mis-replicated blocks:         0 (0.0 %)
 Default replication factor:    3
 Average block replication:     3.0
 Corrupt blocks:                0
 Missing replicas:              0 (0.0 %)
 Number of data-nodes:          3
 Number of racks:               1
FSCK ended at Fri Mar 16 10:09:19 UTC 2018 in 10 milliseconds


The filesystem under path '/user/hilary' is HEALTHY
```