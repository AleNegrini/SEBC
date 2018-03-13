# HDFS Throughput test

## Create end-user Linux
On all the hosts, I created __AleNegrini__ user by typing:
```
[root@amsterdam cloudera]# adduser AleNegrini
```
Create HDFS user directory (command typed on a DataNode): 
```
[hdfs@london cloudera]$ hdfs dfs -mkdir /user/AleNegrini
[hdfs@london cloudera]$ hdfs dfs -ls /user
Found 7 items
drwxr-xr-x   - hdfs   supergroup          0 2018-03-13 11:04 /user/AleNegrini
drwxr-xr-x   - hdfs   supergroup          0 2018-03-13 10:52 /user/AleNegrini_copied
drwx------   - hdfs   supergroup          0 2018-03-13 09:44 /user/hdfs
drwxrwxrwx   - mapred hadoop              0 2018-03-12 17:03 /user/history
drwxrwxr-t   - hive   hive                0 2018-03-12 17:03 /user/hive
drwxrwxr-x   - hue    hue                 0 2018-03-12 17:04 /user/hue
drwxrwxr-x   - oozie  oozie               0 2018-03-12 17:04 /user/oozie
```
Change the ownership of that folder
```
[hdfs@london cloudera]$ hdfs dfs -chown AleNegrini:AleNegrini /user/AleNegrini
[hdfs@london cloudera]$ hdfs dfs -ls /user
Found 7 items
drwxr-xr-x   - AleNegrini AleNegrini          0 2018-03-13 11:04 /user/AleNegrini
drwxr-xr-x   - hdfs       supergroup          0 2018-03-13 10:52 /user/AleNegrini_copied
drwx------   - hdfs       supergroup          0 2018-03-13 09:44 /user/hdfs
drwxrwxrwx   - mapred     hadoop              0 2018-03-12 17:03 /user/history
drwxrwxr-t   - hive       hive                0 2018-03-12 17:03 /user/hive
drwxrwxr-x   - hue        hue                 0 2018-03-12 17:04 /user/hue
drwxrwxr-x   - oozie      oozie               0 2018-03-12 17:04 /user/oozie
```

## Teragen

Command launched with AleNegrini user
```
[AleNegrini@london cloudera]$ time hadoop jar /opt/cloudera/parcels/CDH/jars/hadoop-examples.jar teragen -Ddfs.replication=1 -Dmapreduce.job.maps=4 -Ddfs.blocksize=33554432 107374182 /user/AleNegrini/teragen10GB
18/03/13 11:12:10 INFO client.RMProxy: Connecting to ResourceManager at berlin.c.sebc-labs.internal/10.142.0.3:8032
18/03/13 11:12:10 INFO terasort.TeraSort: Generating 107374182 using 4
18/03/13 11:12:10 INFO mapreduce.JobSubmitter: number of splits:4
18/03/13 11:12:11 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_1520874181129_0010
18/03/13 11:12:11 INFO impl.YarnClientImpl: Submitted application application_1520874181129_0010
18/03/13 11:12:11 INFO mapreduce.Job: The url to track the job: http://berlin.c.sebc-labs.internal:8088/proxy/application_1520874181129_0010/
18/03/13 11:12:11 INFO mapreduce.Job: Running job: job_1520874181129_0010
18/03/13 11:12:18 INFO mapreduce.Job: Job job_1520874181129_0010 running in uber mode : false
18/03/13 11:12:18 INFO mapreduce.Job:  map 0% reduce 0%
18/03/13 11:12:30 INFO mapreduce.Job:  map 3% reduce 0%
18/03/13 11:12:31 INFO mapreduce.Job:  map 7% reduce 0%
18/03/13 11:12:33 INFO mapreduce.Job:  map 12% reduce 0%
18/03/13 11:12:34 INFO mapreduce.Job:  map 15% reduce 0%
18/03/13 11:12:35 INFO mapreduce.Job:  map 16% reduce 0%
18/03/13 11:12:36 INFO mapreduce.Job:  map 19% reduce 0%
18/03/13 11:12:37 INFO mapreduce.Job:  map 22% reduce 0%
18/03/13 11:12:38 INFO mapreduce.Job:  map 23% reduce 0%
18/03/13 11:12:39 INFO mapreduce.Job:  map 27% reduce 0%
18/03/13 11:12:40 INFO mapreduce.Job:  map 29% reduce 0%
18/03/13 11:12:41 INFO mapreduce.Job:  map 31% reduce 0%
18/03/13 11:12:42 INFO mapreduce.Job:  map 34% reduce 0%
18/03/13 11:12:43 INFO mapreduce.Job:  map 37% reduce 0%
18/03/13 11:12:44 INFO mapreduce.Job:  map 38% reduce 0%
18/03/13 11:12:45 INFO mapreduce.Job:  map 42% reduce 0%
18/03/13 11:12:46 INFO mapreduce.Job:  map 45% reduce 0%
18/03/13 11:12:48 INFO mapreduce.Job:  map 50% reduce 0%
18/03/13 11:12:49 INFO mapreduce.Job:  map 53% reduce 0%
18/03/13 11:12:51 INFO mapreduce.Job:  map 58% reduce 0%
18/03/13 11:12:52 INFO mapreduce.Job:  map 60% reduce 0%
18/03/13 11:12:54 INFO mapreduce.Job:  map 65% reduce 0%
18/03/13 11:12:55 INFO mapreduce.Job:  map 68% reduce 0%
18/03/13 11:12:57 INFO mapreduce.Job:  map 74% reduce 0%
18/03/13 11:12:58 INFO mapreduce.Job:  map 75% reduce 0%
18/03/13 11:13:00 INFO mapreduce.Job:  map 78% reduce 0%
18/03/13 11:13:03 INFO mapreduce.Job:  map 80% reduce 0%
18/03/13 11:13:06 INFO mapreduce.Job:  map 83% reduce 0%
18/03/13 11:13:09 INFO mapreduce.Job:  map 86% reduce 0%
18/03/13 11:13:12 INFO mapreduce.Job:  map 89% reduce 0%
18/03/13 11:13:15 INFO mapreduce.Job:  map 91% reduce 0%
18/03/13 11:13:18 INFO mapreduce.Job:  map 94% reduce 0%
18/03/13 11:13:21 INFO mapreduce.Job:  map 97% reduce 0%
18/03/13 11:13:24 INFO mapreduce.Job:  map 100% reduce 0%
18/03/13 11:13:25 INFO mapreduce.Job: Job job_1520874181129_0010 completed successfully
18/03/13 11:13:25 INFO mapreduce.Job: Counters: 31
        File System Counters
                FILE: Number of bytes read=0
                FILE: Number of bytes written=493140
                FILE: Number of read operations=0
                FILE: Number of large read operations=0
                FILE: Number of write operations=0
                HDFS: Number of bytes read=344
                HDFS: Number of bytes written=10737418200
                HDFS: Number of read operations=16
                HDFS: Number of large read operations=0
                HDFS: Number of write operations=8
        Job Counters
                Launched map tasks=4
                Other local map tasks=4
                Total time spent by all maps in occupied slots (ms)=202145
                Total time spent by all reduces in occupied slots (ms)=0
                Total time spent by all map tasks (ms)=202145
                Total vcore-seconds taken by all map tasks=202145
                Total megabyte-seconds taken by all map tasks=206996480
        Map-Reduce Framework
                Map input records=107374182
                Map output records=107374182
                Input split bytes=344
                Spilled Records=0
                Failed Shuffles=0
                Merged Map outputs=0
                GC time elapsed (ms)=2353
                CPU time spent (ms)=170810
                Physical memory (bytes) snapshot=1141514240
                Virtual memory (bytes) snapshot=6276718592
                Total committed heap usage (bytes)=1032847360
        org.apache.hadoop.examples.terasort.TeraGen$Counters
                CHECKSUM=230593859918397906
        File Input Format Counters
                Bytes Read=0
        File Output Format Counters
                Bytes Written=10737418200

real    1m17.853s
user    0m5.030s
sys     0m0.288s
```

Double check that files are there and that the total sum of the produced files gives 10GB.
```
[AleNegrini@london cloudera]$ hdfs dfs -ls /user/AleNegrini/teragen10GB
Found 5 items
-rw-r--r--   1 AleNegrini AleNegrini          0 2018-03-13 11:13 /user/AleNegrini/teragen10GB/_SUCCESS
-rw-r--r--   1 AleNegrini AleNegrini 2684354600 2018-03-13 11:12 /user/AleNegrini/teragen10GB/part-m-00000
-rw-r--r--   1 AleNegrini AleNegrini 2684354500 2018-03-13 11:13 /user/AleNegrini/teragen10GB/part-m-00001
-rw-r--r--   1 AleNegrini AleNegrini 2684354600 2018-03-13 11:13 /user/AleNegrini/teragen10GB/part-m-00002
-rw-r--r--   1 AleNegrini AleNegrini 2684354500 2018-03-13 11:12 /user/AleNegrini/teragen10GB/part-m-00003
```