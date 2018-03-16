# PI after Kerberos

```
[anupam@paris root]$ kinit anupam
Password for anupam@ALENEGRINI.NL:
[anupam@paris root]$ klist
Ticket cache: FILE:/tmp/krb5cc_2900
Default principal: anupam@ALENEGRINI.NL

Valid starting       Expires              Service principal
03/16/2018 11:02:48  03/17/2018 11:02:48  krbtgt/ALENEGRINI.NL@ALENEGRINI.NL
        renew until 03/23/2018 11:02:48
[anupam@paris root]$ hadoop jar /opt/cloudera/parcels/CDH/lib/hadoop-mapreduce/hadoop-mapreduce-examples.jar pi 50 100
Number of Maps  = 50
Samples per Map = 100
Wrote input for Map #0
Wrote input for Map #1
Wrote input for Map #2
Wrote input for Map #3
Wrote input for Map #4
Wrote input for Map #5
Wrote input for Map #6
Wrote input for Map #7
Wrote input for Map #8
Wrote input for Map #9
Wrote input for Map #10
Wrote input for Map #11
Wrote input for Map #12
Wrote input for Map #13
Wrote input for Map #14
Wrote input for Map #15
Wrote input for Map #16
Wrote input for Map #17
Wrote input for Map #18
Wrote input for Map #19
Wrote input for Map #20
Wrote input for Map #21
Wrote input for Map #22
Wrote input for Map #23
Wrote input for Map #24
Wrote input for Map #25
Wrote input for Map #26
Wrote input for Map #27
Wrote input for Map #28
Wrote input for Map #29
Wrote input for Map #30
Wrote input for Map #31
Wrote input for Map #32
Wrote input for Map #33
Wrote input for Map #34
Wrote input for Map #35
Wrote input for Map #36
Wrote input for Map #37
Wrote input for Map #38
Wrote input for Map #39
Wrote input for Map #40
Wrote input for Map #41
Wrote input for Map #42
Wrote input for Map #43
Wrote input for Map #44
Wrote input for Map #45
Wrote input for Map #46
Wrote input for Map #47
Wrote input for Map #48
Wrote input for Map #49
Starting Job
18/03/16 11:07:28 INFO client.RMProxy: Connecting to ResourceManager at berlin.c.sebc-pre-challenges.internal/10.142.0.6:8032
18/03/16 11:07:28 INFO hdfs.DFSClient: Created token for anupam: HDFS_DELEGATION_TOKEN owner=anupam@ALENEGRINI.NL, renewer=yarn, realUser=, issueDate=1521198448273, maxDate=1521803248273, sequenceNumber=3, masterKeyId=2 on 10.142.0.2:8020
18/03/16 11:07:28 INFO security.TokenCache: Got dt for hdfs://amsterdam.c.sebc-pre-challenges.internal:8020; Kind: HDFS_DELEGATION_TOKEN, Service: 10.142.0.2:8020, Ident: (token for anupam: HDFS_DELEGATION_TOKEN owner=anupam@ALENEGRINI.NL, renewer=yarn, realUser=, issueDate=1521198448273, maxDate=1521803248273, sequenceNumber=3, masterKeyId=2)
18/03/16 11:07:28 INFO input.FileInputFormat: Total input paths to process : 50
18/03/16 11:07:28 INFO mapreduce.JobSubmitter: number of splits:50
18/03/16 11:07:28 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_1521197768174_0003
18/03/16 11:07:28 INFO mapreduce.JobSubmitter: Kind: HDFS_DELEGATION_TOKEN, Service: 10.142.0.2:8020, Ident: (token for anupam: HDFS_DELEGATION_TOKEN owner=anupam@ALENEGRINI.NL, renewer=yarn, realUser=, issueDate=1521198448273, maxDate=1521803248273, sequenceNumber=3, masterKeyId=2)
18/03/16 11:07:29 INFO impl.YarnClientImpl: Submitted application application_1521197768174_0003
18/03/16 11:07:29 INFO mapreduce.Job: The url to track the job: http://berlin.c.sebc-pre-challenges.internal:8088/proxy/application_1521197768174_0003/
18/03/16 11:07:29 INFO mapreduce.Job: Running job: job_1521197768174_0003
18/03/16 11:07:39 INFO mapreduce.Job: Job job_1521197768174_0003 running in uber mode : false
18/03/16 11:07:39 INFO mapreduce.Job:  map 0% reduce 0%
18/03/16 11:07:46 INFO mapreduce.Job:  map 2% reduce 0%
18/03/16 11:07:52 INFO mapreduce.Job:  map 4% reduce 0%
18/03/16 11:07:54 INFO mapreduce.Job:  map 12% reduce 0%
18/03/16 11:07:57 INFO mapreduce.Job:  map 14% reduce 0%
18/03/16 11:08:02 INFO mapreduce.Job:  map 18% reduce 0%
18/03/16 11:08:03 INFO mapreduce.Job:  map 24% reduce 0%
18/03/16 11:08:09 INFO mapreduce.Job:  map 26% reduce 0%
18/03/16 11:08:11 INFO mapreduce.Job:  map 30% reduce 0%
18/03/16 11:08:12 INFO mapreduce.Job:  map 34% reduce 0%
18/03/16 11:08:15 INFO mapreduce.Job:  map 36% reduce 0%
18/03/16 11:08:18 INFO mapreduce.Job:  map 38% reduce 0%
18/03/16 11:08:19 INFO mapreduce.Job:  map 40% reduce 0%
18/03/16 11:08:20 INFO mapreduce.Job:  map 42% reduce 0%
18/03/16 11:08:21 INFO mapreduce.Job:  map 46% reduce 0%
18/03/16 11:08:26 INFO mapreduce.Job:  map 50% reduce 0%
18/03/16 11:08:27 INFO mapreduce.Job:  map 52% reduce 0%
18/03/16 11:08:28 INFO mapreduce.Job:  map 54% reduce 0%
18/03/16 11:08:29 INFO mapreduce.Job:  map 56% reduce 0%
18/03/16 11:08:31 INFO mapreduce.Job:  map 58% reduce 0%
18/03/16 11:08:34 INFO mapreduce.Job:  map 62% reduce 0%
18/03/16 11:08:35 INFO mapreduce.Job:  map 64% reduce 0%
18/03/16 11:08:36 INFO mapreduce.Job:  map 66% reduce 0%
18/03/16 11:08:37 INFO mapreduce.Job:  map 68% reduce 0%
18/03/16 11:08:42 INFO mapreduce.Job:  map 70% reduce 0%
18/03/16 11:08:43 INFO mapreduce.Job:  map 74% reduce 0%
18/03/16 11:08:45 INFO mapreduce.Job:  map 76% reduce 0%
18/03/16 11:08:46 INFO mapreduce.Job:  map 78% reduce 0%
18/03/16 11:08:48 INFO mapreduce.Job:  map 80% reduce 0%
18/03/16 11:08:49 INFO mapreduce.Job:  map 82% reduce 0%
18/03/16 11:08:51 INFO mapreduce.Job:  map 84% reduce 0%
18/03/16 11:08:53 INFO mapreduce.Job:  map 90% reduce 0%
18/03/16 11:08:57 INFO mapreduce.Job:  map 92% reduce 0%
18/03/16 11:08:58 INFO mapreduce.Job:  map 94% reduce 0%
18/03/16 11:09:02 INFO mapreduce.Job:  map 100% reduce 0%
18/03/16 11:09:03 INFO mapreduce.Job:  map 100% reduce 100%
18/03/16 11:09:04 INFO mapreduce.Job: Job job_1521197768174_0003 completed successfully
18/03/16 11:09:04 INFO mapreduce.Job: Counters: 49
        File System Counters
                FILE: Number of bytes read=257
                FILE: Number of bytes written=7625626
                FILE: Number of read operations=0
                FILE: Number of large read operations=0
                FILE: Number of write operations=0
                HDFS: Number of bytes read=14790
                HDFS: Number of bytes written=215
                HDFS: Number of read operations=203
                HDFS: Number of large read operations=0
                HDFS: Number of write operations=3
        Job Counters
                Launched map tasks=50
                Launched reduce tasks=1
                Data-local map tasks=50
                Total time spent by all maps in occupied slots (ms)=338372
                Total time spent by all reduces in occupied slots (ms)=11213
                Total time spent by all map tasks (ms)=338372
                Total time spent by all reduce tasks (ms)=11213
                Total vcore-milliseconds taken by all map tasks=338372
                Total vcore-milliseconds taken by all reduce tasks=11213
                Total megabyte-milliseconds taken by all map tasks=346492928
                Total megabyte-milliseconds taken by all reduce tasks=11482112
        Map-Reduce Framework
                Map input records=50
                Map output records=100
                Map output bytes=900
                Map output materialized bytes=1700
                Input split bytes=8890
                Combine input records=0
                Combine output records=0
                Reduce input groups=2
                Reduce shuffle bytes=1700
                Reduce input records=100
                Reduce output records=0
                Spilled Records=200
                Shuffled Maps =50
                Failed Shuffles=0
                Merged Map outputs=50
                GC time elapsed (ms)=3356
                CPU time spent (ms)=36500
                Physical memory (bytes) snapshot=24318164992
                Virtual memory (bytes) snapshot=80459636736
                Total committed heap usage (bytes)=26496466944
        Shuffle Errors
                BAD_ID=0
                CONNECTION=0
                IO_ERROR=0
                WRONG_LENGTH=0
                WRONG_MAP=0
                WRONG_REDUCE=0
        File Input Format Counters
                Bytes Read=5900
        File Output Format Counters
                Bytes Written=97
Job Finished in 96.88 seconds
Estimated value of Pi is 3.14160000000000000000

```