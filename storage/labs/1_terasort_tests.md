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

## Terasort
```
[AleNegrini@london cloudera]$ time hadoop jar /opt/cloudera/parcels/CDH/jars/hadoop-examples.jar terasort /user/AleNegrini/teragen10GB /user/AleNegrini/terasort10GB
18/03/13 12:00:27 INFO terasort.TeraSort: starting
18/03/13 12:00:29 INFO input.FileInputFormat: Total input paths to process : 4
Spent 225ms computing base-splits.
Spent 4ms computing TeraScheduler splits.
Computing input splits took 230ms
Sampling 10 splits of 320
Making 3 from 100000 sampled records
Computing parititions took 1316ms
Spent 1549ms computing partitions.
18/03/13 12:00:30 INFO client.RMProxy: Connecting to ResourceManager at berlin.c.sebc-labs.internal/10.142.0.3:8032
18/03/13 12:00:31 INFO mapreduce.JobSubmitter: number of splits:320
18/03/13 12:00:31 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_1520874181129_0011
18/03/13 12:00:31 INFO impl.YarnClientImpl: Submitted application application_1520874181129_0011
18/03/13 12:00:31 INFO mapreduce.Job: The url to track the job: http://berlin.c.sebc-labs.internal:8088/proxy/application_1520874181129_0011/
18/03/13 12:00:31 INFO mapreduce.Job: Running job: job_1520874181129_0011
18/03/13 12:00:39 INFO mapreduce.Job: Job job_1520874181129_0011 running in uber mode : false
18/03/13 12:00:39 INFO mapreduce.Job:  map 0% reduce 0%
18/03/13 12:00:51 INFO mapreduce.Job:  map 1% reduce 0%
18/03/13 12:00:53 INFO mapreduce.Job:  map 2% reduce 0%
18/03/13 12:01:04 INFO mapreduce.Job:  map 3% reduce 0%
18/03/13 12:01:09 INFO mapreduce.Job:  map 4% reduce 0%
18/03/13 12:01:16 INFO mapreduce.Job:  map 5% reduce 0%
18/03/13 12:01:24 INFO mapreduce.Job:  map 6% reduce 0%
18/03/13 12:01:28 INFO mapreduce.Job:  map 7% reduce 0%
18/03/13 12:01:37 INFO mapreduce.Job:  map 8% reduce 0%
18/03/13 12:01:39 INFO mapreduce.Job:  map 9% reduce 0%
18/03/13 12:01:49 INFO mapreduce.Job:  map 10% reduce 0%
18/03/13 12:01:52 INFO mapreduce.Job:  map 11% reduce 0%
18/03/13 12:01:59 INFO mapreduce.Job:  map 12% reduce 0%
18/03/13 12:02:06 INFO mapreduce.Job:  map 13% reduce 0%
18/03/13 12:02:13 INFO mapreduce.Job:  map 14% reduce 0%
18/03/13 12:02:20 INFO mapreduce.Job:  map 15% reduce 0%
18/03/13 12:02:23 INFO mapreduce.Job:  map 16% reduce 0%
18/03/13 12:02:32 INFO mapreduce.Job:  map 17% reduce 0%
18/03/13 12:02:41 INFO mapreduce.Job:  map 18% reduce 0%
18/03/13 12:02:46 INFO mapreduce.Job:  map 19% reduce 0%
18/03/13 12:02:53 INFO mapreduce.Job:  map 20% reduce 0%
18/03/13 12:02:57 INFO mapreduce.Job:  map 21% reduce 0%
18/03/13 12:03:04 INFO mapreduce.Job:  map 22% reduce 0%
18/03/13 12:03:09 INFO mapreduce.Job:  map 23% reduce 0%
18/03/13 12:03:16 INFO mapreduce.Job:  map 24% reduce 0%
18/03/13 12:03:24 INFO mapreduce.Job:  map 25% reduce 0%
18/03/13 12:03:31 INFO mapreduce.Job:  map 26% reduce 0%
18/03/13 12:03:37 INFO mapreduce.Job:  map 27% reduce 0%
18/03/13 12:03:42 INFO mapreduce.Job:  map 28% reduce 0%
18/03/13 12:03:50 INFO mapreduce.Job:  map 29% reduce 0%
18/03/13 12:03:54 INFO mapreduce.Job:  map 30% reduce 0%
18/03/13 12:04:01 INFO mapreduce.Job:  map 31% reduce 0%
18/03/13 12:04:06 INFO mapreduce.Job:  map 32% reduce 0%
18/03/13 12:04:15 INFO mapreduce.Job:  map 33% reduce 0%
18/03/13 12:04:22 INFO mapreduce.Job:  map 34% reduce 0%
18/03/13 12:04:27 INFO mapreduce.Job:  map 35% reduce 0%
18/03/13 12:04:35 INFO mapreduce.Job:  map 36% reduce 0%
18/03/13 12:04:38 INFO mapreduce.Job:  map 37% reduce 0%
18/03/13 12:04:45 INFO mapreduce.Job:  map 38% reduce 0%
18/03/13 12:04:55 INFO mapreduce.Job:  map 39% reduce 0%
18/03/13 12:04:59 INFO mapreduce.Job:  map 40% reduce 0%
18/03/13 12:05:07 INFO mapreduce.Job:  map 41% reduce 0%
18/03/13 12:05:10 INFO mapreduce.Job:  map 42% reduce 0%
18/03/13 12:05:18 INFO mapreduce.Job:  map 43% reduce 0%
18/03/13 12:05:25 INFO mapreduce.Job:  map 44% reduce 0%
18/03/13 12:05:31 INFO mapreduce.Job:  map 45% reduce 0%
18/03/13 12:05:38 INFO mapreduce.Job:  map 46% reduce 0%
18/03/13 12:05:43 INFO mapreduce.Job:  map 47% reduce 0%
18/03/13 12:05:53 INFO mapreduce.Job:  map 48% reduce 0%
18/03/13 12:05:56 INFO mapreduce.Job:  map 49% reduce 0%
18/03/13 12:06:02 INFO mapreduce.Job:  map 50% reduce 0%
18/03/13 12:06:07 INFO mapreduce.Job:  map 51% reduce 0%
18/03/13 12:06:14 INFO mapreduce.Job:  map 52% reduce 0%
18/03/13 12:06:21 INFO mapreduce.Job:  map 53% reduce 0%
18/03/13 12:06:29 INFO mapreduce.Job:  map 54% reduce 0%
18/03/13 12:06:35 INFO mapreduce.Job:  map 55% reduce 0%
18/03/13 12:06:41 INFO mapreduce.Job:  map 56% reduce 0%
18/03/13 12:06:45 INFO mapreduce.Job:  map 57% reduce 0%
18/03/13 12:06:53 INFO mapreduce.Job:  map 58% reduce 0%
18/03/13 12:07:03 INFO mapreduce.Job:  map 59% reduce 0%
18/03/13 12:07:05 INFO mapreduce.Job:  map 60% reduce 0%
18/03/13 12:07:13 INFO mapreduce.Job:  map 61% reduce 0%
18/03/13 12:07:17 INFO mapreduce.Job:  map 62% reduce 0%
18/03/13 12:07:26 INFO mapreduce.Job:  map 63% reduce 0%
18/03/13 12:07:34 INFO mapreduce.Job:  map 64% reduce 0%
18/03/13 12:07:37 INFO mapreduce.Job:  map 65% reduce 0%
18/03/13 12:07:45 INFO mapreduce.Job:  map 66% reduce 0%
18/03/13 12:07:49 INFO mapreduce.Job:  map 67% reduce 0%
18/03/13 12:07:57 INFO mapreduce.Job:  map 68% reduce 0%
18/03/13 12:08:03 INFO mapreduce.Job:  map 69% reduce 0%
18/03/13 12:08:10 INFO mapreduce.Job:  map 70% reduce 0%
18/03/13 12:08:18 INFO mapreduce.Job:  map 71% reduce 0%
18/03/13 12:08:22 INFO mapreduce.Job:  map 72% reduce 0%
18/03/13 12:08:29 INFO mapreduce.Job:  map 73% reduce 0%
18/03/13 12:08:34 INFO mapreduce.Job:  map 74% reduce 0%
18/03/13 12:08:41 INFO mapreduce.Job:  map 75% reduce 0%
18/03/13 12:08:46 INFO mapreduce.Job:  map 76% reduce 0%
18/03/13 12:08:53 INFO mapreduce.Job:  map 77% reduce 0%
18/03/13 12:09:02 INFO mapreduce.Job:  map 78% reduce 0%
18/03/13 12:09:07 INFO mapreduce.Job:  map 79% reduce 0%
18/03/13 12:09:14 INFO mapreduce.Job:  map 80% reduce 0%
18/03/13 12:09:19 INFO mapreduce.Job:  map 81% reduce 0%
18/03/13 12:09:26 INFO mapreduce.Job:  map 82% reduce 0%
18/03/13 12:09:32 INFO mapreduce.Job:  map 82% reduce 2%
18/03/13 12:09:36 INFO mapreduce.Job:  map 82% reduce 3%
18/03/13 12:09:38 INFO mapreduce.Job:  map 83% reduce 3%
18/03/13 12:09:40 INFO mapreduce.Job:  map 83% reduce 4%
18/03/13 12:09:42 INFO mapreduce.Job:  map 83% reduce 5%
18/03/13 12:09:43 INFO mapreduce.Job:  map 83% reduce 6%
18/03/13 12:09:45 INFO mapreduce.Job:  map 83% reduce 7%
18/03/13 12:09:48 INFO mapreduce.Job:  map 83% reduce 8%
18/03/13 12:09:49 INFO mapreduce.Job:  map 84% reduce 9%
18/03/13 12:09:51 INFO mapreduce.Job:  map 84% reduce 10%
18/03/13 12:09:55 INFO mapreduce.Job:  map 84% reduce 11%
18/03/13 12:09:56 INFO mapreduce.Job:  map 85% reduce 11%
18/03/13 12:09:57 INFO mapreduce.Job:  map 85% reduce 12%
18/03/13 12:09:59 INFO mapreduce.Job:  map 85% reduce 13%
18/03/13 12:10:04 INFO mapreduce.Job:  map 85% reduce 14%
18/03/13 12:10:05 INFO mapreduce.Job:  map 86% reduce 15%
18/03/13 12:10:06 INFO mapreduce.Job:  map 86% reduce 16%
18/03/13 12:10:10 INFO mapreduce.Job:  map 86% reduce 17%
18/03/13 12:10:12 INFO mapreduce.Job:  map 86% reduce 18%
18/03/13 12:10:14 INFO mapreduce.Job:  map 87% reduce 18%
18/03/13 12:10:16 INFO mapreduce.Job:  map 87% reduce 19%
18/03/13 12:10:22 INFO mapreduce.Job:  map 88% reduce 19%
18/03/13 12:10:29 INFO mapreduce.Job:  map 88% reduce 20%
18/03/13 12:10:32 INFO mapreduce.Job:  map 89% reduce 20%
18/03/13 12:10:39 INFO mapreduce.Job:  map 90% reduce 20%
18/03/13 12:10:47 INFO mapreduce.Job:  map 91% reduce 20%
18/03/13 12:10:55 INFO mapreduce.Job:  map 92% reduce 20%
18/03/13 12:11:04 INFO mapreduce.Job:  map 93% reduce 20%
18/03/13 12:11:05 INFO mapreduce.Job:  map 93% reduce 21%
18/03/13 12:11:12 INFO mapreduce.Job:  map 94% reduce 21%
18/03/13 12:11:19 INFO mapreduce.Job:  map 95% reduce 21%
18/03/13 12:11:26 INFO mapreduce.Job:  map 96% reduce 21%
18/03/13 12:11:34 INFO mapreduce.Job:  map 97% reduce 21%
18/03/13 12:11:39 INFO mapreduce.Job:  map 97% reduce 22%
18/03/13 12:11:43 INFO mapreduce.Job:  map 98% reduce 22%
18/03/13 12:11:51 INFO mapreduce.Job:  map 99% reduce 22%
18/03/13 12:11:59 INFO mapreduce.Job:  map 100% reduce 22%
18/03/13 12:12:02 INFO mapreduce.Job:  map 100% reduce 33%
18/03/13 12:12:03 INFO mapreduce.Job:  map 100% reduce 44%
18/03/13 12:12:05 INFO mapreduce.Job:  map 100% reduce 45%
18/03/13 12:12:08 INFO mapreduce.Job:  map 100% reduce 46%
18/03/13 12:12:09 INFO mapreduce.Job:  map 100% reduce 48%
18/03/13 12:12:11 INFO mapreduce.Job:  map 100% reduce 49%
18/03/13 12:12:14 INFO mapreduce.Job:  map 100% reduce 50%
18/03/13 12:12:15 INFO mapreduce.Job:  map 100% reduce 51%
18/03/13 12:12:17 INFO mapreduce.Job:  map 100% reduce 52%
18/03/13 12:12:20 INFO mapreduce.Job:  map 100% reduce 53%
18/03/13 12:12:21 INFO mapreduce.Job:  map 100% reduce 55%
18/03/13 12:12:24 INFO mapreduce.Job:  map 100% reduce 56%
18/03/13 12:12:26 INFO mapreduce.Job:  map 100% reduce 57%
18/03/13 12:12:27 INFO mapreduce.Job:  map 100% reduce 58%
18/03/13 12:12:29 INFO mapreduce.Job:  map 100% reduce 59%
18/03/13 12:12:30 INFO mapreduce.Job:  map 100% reduce 60%
18/03/13 12:12:33 INFO mapreduce.Job:  map 100% reduce 62%
18/03/13 12:12:35 INFO mapreduce.Job:  map 100% reduce 63%
18/03/13 12:12:38 INFO mapreduce.Job:  map 100% reduce 64%
18/03/13 12:12:39 INFO mapreduce.Job:  map 100% reduce 65%
18/03/13 12:12:41 INFO mapreduce.Job:  map 100% reduce 66%
18/03/13 12:12:42 INFO mapreduce.Job:  map 100% reduce 67%
18/03/13 12:12:44 INFO mapreduce.Job:  map 100% reduce 68%
18/03/13 12:12:45 INFO mapreduce.Job:  map 100% reduce 69%
18/03/13 12:12:47 INFO mapreduce.Job:  map 100% reduce 70%
18/03/13 12:12:48 INFO mapreduce.Job:  map 100% reduce 71%
18/03/13 12:12:51 INFO mapreduce.Job:  map 100% reduce 72%
18/03/13 12:12:54 INFO mapreduce.Job:  map 100% reduce 73%
18/03/13 12:12:57 INFO mapreduce.Job:  map 100% reduce 74%
18/03/13 12:13:00 INFO mapreduce.Job:  map 100% reduce 75%
18/03/13 12:13:03 INFO mapreduce.Job:  map 100% reduce 84%
18/03/13 12:13:06 INFO mapreduce.Job:  map 100% reduce 87%
18/03/13 12:13:09 INFO mapreduce.Job:  map 100% reduce 88%
18/03/13 12:13:12 INFO mapreduce.Job:  map 100% reduce 89%
18/03/13 12:13:15 INFO mapreduce.Job:  map 100% reduce 90%
18/03/13 12:13:18 INFO mapreduce.Job:  map 100% reduce 91%
18/03/13 12:13:24 INFO mapreduce.Job:  map 100% reduce 92%
18/03/13 12:13:27 INFO mapreduce.Job:  map 100% reduce 93%
18/03/13 12:13:30 INFO mapreduce.Job:  map 100% reduce 94%
18/03/13 12:13:33 INFO mapreduce.Job:  map 100% reduce 95%
18/03/13 12:13:39 INFO mapreduce.Job:  map 100% reduce 96%
18/03/13 12:13:42 INFO mapreduce.Job:  map 100% reduce 97%
18/03/13 12:13:45 INFO mapreduce.Job:  map 100% reduce 98%
18/03/13 12:13:48 INFO mapreduce.Job:  map 100% reduce 99%
18/03/13 12:13:54 INFO mapreduce.Job:  map 100% reduce 100%
18/03/13 12:13:54 INFO mapreduce.Job: Job job_1520874181129_0011 completed successfully
18/03/13 12:13:54 INFO mapreduce.Job: Counters: 50
        File System Counters
                FILE: Number of bytes read=4795343304
                FILE: Number of bytes written=9498425273
                FILE: Number of read operations=0
                FILE: Number of large read operations=0
                FILE: Number of write operations=0
                HDFS: Number of bytes read=10737465560
                HDFS: Number of bytes written=10737418200
                HDFS: Number of read operations=969
                HDFS: Number of large read operations=0
                HDFS: Number of write operations=6
        Job Counters
                Launched map tasks=320
                Launched reduce tasks=3
                Data-local map tasks=254
                Rack-local map tasks=66
                Total time spent by all maps in occupied slots (ms)=2692430
                Total time spent by all reduces in occupied slots (ms)=558062
                Total time spent by all map tasks (ms)=2692430
                Total time spent by all reduce tasks (ms)=558062
                Total vcore-seconds taken by all map tasks=2692430
                Total vcore-seconds taken by all reduce tasks=558062
                Total megabyte-seconds taken by all map tasks=2757048320
                Total megabyte-seconds taken by all reduce tasks=571455488
        Map-Reduce Framework
                Map input records=107374182
                Map output records=107374182
                Map output bytes=10952166564
                Map output materialized bytes=4662781941
                Input split bytes=47360
                Combine input records=0
                Combine output records=0
                Reduce input groups=107374182
                Reduce shuffle bytes=4662781941
                Reduce input records=107374182
                Reduce output records=107374182
                Spilled Records=214748364
                Shuffled Maps =960
                Failed Shuffles=0
                Merged Map outputs=960
                GC time elapsed (ms)=45675
                CPU time spent (ms)=1396280
                Physical memory (bytes) snapshot=160819040256
                Virtual memory (bytes) snapshot=508703473664
                Total committed heap usage (bytes)=197218795520
        Shuffle Errors
                BAD_ID=0
                CONNECTION=0
                IO_ERROR=0
                WRONG_LENGTH=0
                WRONG_MAP=0
                WRONG_REDUCE=0
        File Input Format Counters
                Bytes Read=10737418200
        File Output Format Counters
                Bytes Written=10737418200
18/03/13 12:13:54 INFO terasort.TeraSort: done

real    13m28.270s
user    0m10.398s
sys     0m0.769s
```