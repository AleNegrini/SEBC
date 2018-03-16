# Terasort after Kerberos

```
[root@milan ~]# hadoop jar /opt/cloudera/parcels/CDH/jars/hadoop-examples.jar te                                                               rasort /user/hilary/tgen /user/hilary/tsort
18/03/16 10:58:24 INFO terasort.TeraSort: starting
18/03/16 10:58:25 INFO hdfs.DFSClient: Created token for hilary: HDFS_DELEGATION                                                               _TOKEN owner=hilary@ALENEGRINI.NL, renewer=yarn, realUser=, issueDate=1521197905                                                               672, maxDate=1521802705672, sequenceNumber=1, masterKeyId=2 on 10.142.0.2:8020
18/03/16 10:58:25 INFO security.TokenCache: Got dt for hdfs://amsterdam.c.sebc-p                                                               re-challenges.internal:8020; Kind: HDFS_DELEGATION_TOKEN, Service: 10.142.0.2:80                                                               20, Ident: (token for hilary: HDFS_DELEGATION_TOKEN owner=hilary@ALENEGRINI.NL,                                                                renewer=yarn, realUser=, issueDate=1521197905672, maxDate=1521802705672, sequenc                                                               eNumber=1, masterKeyId=2)
18/03/16 10:58:25 INFO input.FileInputFormat: Total input paths to process : 16
Spent 346ms computing base-splits.
Spent 4ms computing TeraScheduler splits.
Computing input splits took 351ms
Sampling 10 splits of 112
Making 3 from 100000 sampled records
Computing parititions took 1174ms
Spent 1527ms computing partitions.
18/03/16 10:58:27 INFO client.RMProxy: Connecting to ResourceManager at berlin.c                                                               .sebc-pre-challenges.internal/10.142.0.6:8032
18/03/16 10:58:27 INFO mapreduce.JobSubmitter: number of splits:112
18/03/16 10:58:28 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_15                                                               21197768174_0001
18/03/16 10:58:28 INFO mapreduce.JobSubmitter: Kind: HDFS_DELEGATION_TOKEN, Serv                                                               ice: 10.142.0.2:8020, Ident: (token for hilary: HDFS_DELEGATION_TOKEN owner=hila                                                               ry@ALENEGRINI.NL, renewer=yarn, realUser=, issueDate=1521197905672, maxDate=1521                                                               802705672, sequenceNumber=1, masterKeyId=2)
18/03/16 10:58:29 INFO impl.YarnClientImpl: Submitted application application_15                                                               21197768174_0001
18/03/16 10:58:29 INFO mapreduce.Job: The url to track the job: http://berlin.c.                                                               sebc-pre-challenges.internal:8088/proxy/application_1521197768174_0001/
18/03/16 10:58:29 INFO mapreduce.Job: Running job: job_1521197768174_0001
18/03/16 10:58:40 INFO mapreduce.Job: Job job_1521197768174_0001 running in uber                                                                mode : false
18/03/16 10:58:40 INFO mapreduce.Job:  map 0% reduce 0%
18/03/16 10:58:49 INFO mapreduce.Job:  map 1% reduce 0%
18/03/16 10:58:57 INFO mapreduce.Job:  map 2% reduce 0%
18/03/16 10:59:00 INFO mapreduce.Job:  map 4% reduce 0%
18/03/16 10:59:02 INFO mapreduce.Job:  map 5% reduce 0%
18/03/16 10:59:05 INFO mapreduce.Job:  map 6% reduce 0%
18/03/16 10:59:14 INFO mapreduce.Job:  map 7% reduce 0%
18/03/16 10:59:15 INFO mapreduce.Job:  map 9% reduce 0%
18/03/16 10:59:16 INFO mapreduce.Job:  map 11% reduce 0%
18/03/16 10:59:21 INFO mapreduce.Job:  map 12% reduce 0%
18/03/16 10:59:27 INFO mapreduce.Job:  map 13% reduce 0%
18/03/16 10:59:30 INFO mapreduce.Job:  map 16% reduce 0%
18/03/16 10:59:38 INFO mapreduce.Job:  map 17% reduce 0%
18/03/16 10:59:41 INFO mapreduce.Job:  map 19% reduce 0%
18/03/16 10:59:44 INFO mapreduce.Job:  map 21% reduce 0%
18/03/16 10:59:53 INFO mapreduce.Job:  map 24% reduce 0%
18/03/16 10:59:58 INFO mapreduce.Job:  map 25% reduce 0%
18/03/16 10:59:59 INFO mapreduce.Job:  map 26% reduce 0%
18/03/16 11:00:02 INFO mapreduce.Job:  map 27% reduce 0%
18/03/16 11:00:07 INFO mapreduce.Job:  map 29% reduce 0%
18/03/16 11:00:10 INFO mapreduce.Job:  map 30% reduce 0%
18/03/16 11:00:12 INFO mapreduce.Job:  map 31% reduce 0%
18/03/16 11:00:19 INFO mapreduce.Job:  map 32% reduce 0%
18/03/16 11:00:20 INFO mapreduce.Job:  map 34% reduce 0%
18/03/16 11:00:24 INFO mapreduce.Job:  map 35% reduce 0%
18/03/16 11:00:26 INFO mapreduce.Job:  map 37% reduce 0%
18/03/16 11:00:33 INFO mapreduce.Job:  map 38% reduce 0%
18/03/16 11:00:34 INFO mapreduce.Job:  map 39% reduce 0%
18/03/16 11:00:37 INFO mapreduce.Job:  map 40% reduce 0%
18/03/16 11:00:38 INFO mapreduce.Job:  map 41% reduce 0%
18/03/16 11:00:42 INFO mapreduce.Job:  map 42% reduce 0%
18/03/16 11:00:46 INFO mapreduce.Job:  map 43% reduce 0%
18/03/16 11:00:47 INFO mapreduce.Job:  map 44% reduce 0%
18/03/16 11:00:50 INFO mapreduce.Job:  map 45% reduce 0%
18/03/16 11:00:51 INFO mapreduce.Job:  map 46% reduce 0%
18/03/16 11:00:59 INFO mapreduce.Job:  map 48% reduce 0%
18/03/16 11:01:00 INFO mapreduce.Job:  map 49% reduce 0%
18/03/16 11:01:03 INFO mapreduce.Job:  map 50% reduce 0%
18/03/16 11:01:04 INFO mapreduce.Job:  map 51% reduce 0%
18/03/16 11:01:07 INFO mapreduce.Job:  map 52% reduce 0%
18/03/16 11:01:12 INFO mapreduce.Job:  map 54% reduce 0%
18/03/16 11:01:18 INFO mapreduce.Job:  map 56% reduce 0%
18/03/16 11:01:24 INFO mapreduce.Job:  map 57% reduce 0%
18/03/16 11:01:25 INFO mapreduce.Job:  map 58% reduce 0%
18/03/16 11:01:26 INFO mapreduce.Job:  map 59% reduce 0%
18/03/16 11:01:30 INFO mapreduce.Job:  map 60% reduce 0%
18/03/16 11:01:31 INFO mapreduce.Job:  map 62% reduce 0%
18/03/16 11:01:39 INFO mapreduce.Job:  map 63% reduce 0%
18/03/16 11:01:40 INFO mapreduce.Job:  map 64% reduce 0%
18/03/16 11:01:44 INFO mapreduce.Job:  map 65% reduce 0%
18/03/16 11:01:45 INFO mapreduce.Job:  map 66% reduce 0%
18/03/16 11:01:48 INFO mapreduce.Job:  map 67% reduce 0%
18/03/16 11:01:52 INFO mapreduce.Job:  map 69% reduce 0%
18/03/16 11:01:56 INFO mapreduce.Job:  map 70% reduce 0%
18/03/16 11:01:57 INFO mapreduce.Job:  map 71% reduce 0%
18/03/16 11:02:05 INFO mapreduce.Job:  map 72% reduce 0%
18/03/16 11:02:06 INFO mapreduce.Job:  map 74% reduce 0%
18/03/16 11:02:11 INFO mapreduce.Job:  map 75% reduce 0%
18/03/16 11:02:12 INFO mapreduce.Job:  map 77% reduce 0%
18/03/16 11:02:18 INFO mapreduce.Job:  map 78% reduce 0%
18/03/16 11:02:19 INFO mapreduce.Job:  map 79% reduce 0%
18/03/16 11:02:24 INFO mapreduce.Job:  map 80% reduce 0%
18/03/16 11:02:25 INFO mapreduce.Job:  map 81% reduce 0%
18/03/16 11:02:29 INFO mapreduce.Job:  map 82% reduce 0%
18/03/16 11:02:31 INFO mapreduce.Job:  map 83% reduce 0%
18/03/16 11:02:32 INFO mapreduce.Job:  map 84% reduce 0%
18/03/16 11:02:37 INFO mapreduce.Job:  map 85% reduce 0%
18/03/16 11:02:38 INFO mapreduce.Job:  map 86% reduce 0%
18/03/16 11:02:41 INFO mapreduce.Job:  map 87% reduce 0%
18/03/16 11:02:45 INFO mapreduce.Job:  map 88% reduce 4%
18/03/16 11:02:50 INFO mapreduce.Job:  map 89% reduce 4%
18/03/16 11:02:51 INFO mapreduce.Job:  map 90% reduce 6%
18/03/16 11:02:52 INFO mapreduce.Job:  map 90% reduce 11%
18/03/16 11:02:57 INFO mapreduce.Job:  map 91% reduce 11%
18/03/16 11:02:58 INFO mapreduce.Job:  map 91% reduce 13%
18/03/16 11:02:59 INFO mapreduce.Job:  map 92% reduce 15%
18/03/16 11:03:02 INFO mapreduce.Job:  map 93% reduce 15%
18/03/16 11:03:03 INFO mapreduce.Job:  map 93% reduce 17%
18/03/16 11:03:05 INFO mapreduce.Job:  map 94% reduce 19%
18/03/16 11:03:07 INFO mapreduce.Job:  map 95% reduce 19%
18/03/16 11:03:09 INFO mapreduce.Job:  map 95% reduce 20%
18/03/16 11:03:10 INFO mapreduce.Job:  map 95% reduce 21%
18/03/16 11:03:11 INFO mapreduce.Job:  map 96% reduce 21%
18/03/16 11:03:15 INFO mapreduce.Job:  map 97% reduce 21%
18/03/16 11:03:17 INFO mapreduce.Job:  map 97% reduce 22%
18/03/16 11:03:18 INFO mapreduce.Job:  map 99% reduce 22%
18/03/16 11:03:24 INFO mapreduce.Job:  map 100% reduce 22%
18/03/16 11:03:28 INFO mapreduce.Job:  map 100% reduce 34%
18/03/16 11:03:29 INFO mapreduce.Job:  map 100% reduce 45%
18/03/16 11:03:33 INFO mapreduce.Job:  map 100% reduce 47%
18/03/16 11:03:35 INFO mapreduce.Job:  map 100% reduce 49%
18/03/16 11:03:37 INFO mapreduce.Job:  map 100% reduce 53%
18/03/16 11:03:39 INFO mapreduce.Job:  map 100% reduce 56%
18/03/16 11:03:41 INFO mapreduce.Job:  map 100% reduce 57%
18/03/16 11:03:44 INFO mapreduce.Job:  map 100% reduce 59%
18/03/16 11:03:46 INFO mapreduce.Job:  map 100% reduce 61%
18/03/16 11:03:47 INFO mapreduce.Job:  map 100% reduce 63%
18/03/16 11:03:50 INFO mapreduce.Job:  map 100% reduce 65%
18/03/16 11:03:52 INFO mapreduce.Job:  map 100% reduce 67%
18/03/16 11:03:53 INFO mapreduce.Job:  map 100% reduce 69%
18/03/16 11:03:55 INFO mapreduce.Job:  map 100% reduce 70%
18/03/16 11:03:56 INFO mapreduce.Job:  map 100% reduce 72%
18/03/16 11:03:59 INFO mapreduce.Job:  map 100% reduce 74%
18/03/16 11:04:01 INFO mapreduce.Job:  map 100% reduce 75%
18/03/16 11:04:05 INFO mapreduce.Job:  map 100% reduce 77%
18/03/16 11:04:07 INFO mapreduce.Job:  map 100% reduce 88%
18/03/16 11:04:11 INFO mapreduce.Job:  map 100% reduce 90%
18/03/16 11:04:14 INFO mapreduce.Job:  map 100% reduce 91%
18/03/16 11:04:20 INFO mapreduce.Job:  map 100% reduce 94%
18/03/16 11:04:26 INFO mapreduce.Job:  map 100% reduce 97%
18/03/16 11:04:32 INFO mapreduce.Job:  map 100% reduce 100%
18/03/16 11:04:34 INFO mapreduce.Job: Job job_1521197768174_0001 completed successfully
18/03/16 11:04:34 INFO mapreduce.Job: Counters: 49
        File System Counters
                FILE: Number of bytes read=2922392006
                FILE: Number of bytes written=5791423450
                FILE: Number of read operations=0
                FILE: Number of large read operations=0
                FILE: Number of write operations=0
                HDFS: Number of bytes read=6553616464
                HDFS: Number of bytes written=6553600000
                HDFS: Number of read operations=345
                HDFS: Number of large read operations=0
                HDFS: Number of write operations=6
        Job Counters
                Launched map tasks=112
                Launched reduce tasks=3
                Data-local map tasks=112
                Total time spent by all maps in occupied slots (ms)=1156032
                Total time spent by all reduces in occupied slots (ms)=257293
                Total time spent by all map tasks (ms)=1156032
                Total time spent by all reduce tasks (ms)=257293
                Total vcore-milliseconds taken by all map tasks=1156032
                Total vcore-milliseconds taken by all reduce tasks=257293
                Total megabyte-milliseconds taken by all map tasks=1183776768
                Total megabyte-milliseconds taken by all reduce tasks=263468032
        Map-Reduce Framework
                Map input records=65536000
                Map output records=65536000
                Map output bytes=6684672000
                Map output materialized bytes=2851743278
                Input split bytes=16464
                Combine input records=0
                Combine output records=0
                Reduce input groups=65536000
                Reduce shuffle bytes=2851743278
                Reduce input records=65536000
                Reduce output records=65536000
                Spilled Records=131072000
                Shuffled Maps =336
                Failed Shuffles=0
                Merged Map outputs=336
                GC time elapsed (ms)=18697
                CPU time spent (ms)=714130
                Physical memory (bytes) snapshot=59822546944
                Virtual memory (bytes) snapshot=181231329280
                Total committed heap usage (bytes)=71432667136
        Shuffle Errors
                BAD_ID=0
                CONNECTION=0
                IO_ERROR=0
                WRONG_LENGTH=0
                WRONG_MAP=0
                WRONG_REDUCE=0
        File Input Format Counters
                Bytes Read=6553600000
        File Output Format Counters
                Bytes Written=6553600000
18/03/16 11:04:34 INFO terasort.TeraSort: done

```

```
[root@milan ~]# hdfs dfs -ls /user/hilary
Found 4 items
drwx------   - hilary supergroup          0 2018-03-16 11:00 /user/hilary/.Trash
drwx------   - hilary supergroup          0 2018-03-16 11:04 /user/hilary/.staging
drwxr-xr-x   - hilary supergroup          0 2018-03-16 10:07 /user/hilary/tgen
drwxr-xr-x   - hilary supergroup          0 2018-03-16 11:04 /user/hilary/tsort
```
