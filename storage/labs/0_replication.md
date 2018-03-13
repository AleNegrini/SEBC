# Replication

## HDFS folder creation with GitHub handle
Get actual hdfs folder tree 
```
[cloudera@london ~]$ sudo su hdfs
[hdfs@london cloudera]$ hdfs dfs -ls /
Found 2 items
drwxrwxrwt   - hdfs supergroup          0 2018-03-12 17:04 /tmp
drwxr-xr-x   - hdfs supergroup          0 2018-03-12 17:04 /user
```
Create hdfs folder with Github handle (mine and my partner)
```
[hdfs@london cloudera]$ hdfs dfs -mkdir /AleNegrini
[hdfs@london cloudera]$ hdfs dfs -mkdir /jconca
```
And finally let's check that the folder has been created with the right ownership:
```
[hdfs@london cloudera]$ hdfs dfs -ls /
Found 4 items
drwxr-xr-x   - hdfs supergroup          0 2018-03-13 09:25 /AleNegrini
drwxr-xr-x   - hdfs supergroup          0 2018-03-13 09:34 /jconca
drwxrwxrwt   - hdfs supergroup          0 2018-03-12 17:04 /tmp
drwxr-xr-x   - hdfs supergroup          0 2018-03-12 17:04 /user
```

Doing the same

## Teragen generation
Teragen accepts as command option the number of rows.
Each row produced by teragen is 100B long.
Therefore in order to produce a 500MB file long, we should to produce 5242880 rows. For sake of simplicity I keep replication equal to 1 and num mappers equal to the number of disks I have for the datanodes (3)

```
[hdfs@london cloudera]$ hadoop jar /opt/cloudera/parcels/CDH/jars/hadoop-examples.jar teragen -Ddfs.replication=1 -Dmapreduce.job.maps=3 5242880 /AleNegrini
18/03/13 09:44:41 INFO client.RMProxy: Connecting to ResourceManager at berlin.c.sebc-labs.internal/10.142.0.3:8032
18/03/13 09:44:42 INFO terasort.TeraSort: Generating 5242880 using 3
18/03/13 09:44:42 INFO mapreduce.JobSubmitter: number of splits:3
18/03/13 09:44:42 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_1520874181129_0001
18/03/13 09:44:43 INFO impl.YarnClientImpl: Submitted application application_1520874181129_0001
18/03/13 09:44:43 INFO mapreduce.Job: The url to track the job: http://berlin.c.sebc-labs.internal:8088/proxy/application_1520874181129_0001/
18/03/13 09:44:43 INFO mapreduce.Job: Running job: job_1520874181129_0001
18/03/13 09:44:51 INFO mapreduce.Job: Job job_1520874181129_0001 running in uber mode : false
18/03/13 09:44:51 INFO mapreduce.Job:  map 0% reduce 0%
18/03/13 09:45:02 INFO mapreduce.Job:  map 33% reduce 0%
18/03/13 09:45:08 INFO mapreduce.Job:  map 100% reduce 0%
18/03/13 09:45:09 INFO mapreduce.Job: Job job_1520874181129_0001 completed successfully
18/03/13 09:45:09 INFO mapreduce.Job: Counters: 31
        File System Counters
                FILE: Number of bytes read=0
                FILE: Number of bytes written=369789
                FILE: Number of read operations=0
                FILE: Number of large read operations=0
                FILE: Number of write operations=0
                HDFS: Number of bytes read=252
                HDFS: Number of bytes written=524288000
                HDFS: Number of read operations=12
                HDFS: Number of large read operations=0
                HDFS: Number of write operations=6
        Job Counters
                Launched map tasks=3
                Other local map tasks=3
                Total time spent by all maps in occupied slots (ms)=36885
                Total time spent by all reduces in occupied slots (ms)=0
                Total time spent by all map tasks (ms)=36885
                Total vcore-seconds taken by all map tasks=36885
                Total megabyte-seconds taken by all map tasks=37770240
        Map-Reduce Framework
                Map input records=5242880
                Map output records=5242880
                Input split bytes=252
                Spilled Records=0
                Failed Shuffles=0
                Merged Map outputs=0
                GC time elapsed (ms)=537
                CPU time spent (ms)=16280
                Physical memory (bytes) snapshot=994013184
                Virtual memory (bytes) snapshot=4726841344
                Total committed heap usage (bytes)=1242038272
        org.apache.hadoop.examples.terasort.TeraGen$Counters
                CHECKSUM=11257830824958050
        File Input Format Counters
                Bytes Read=0
        File Output Format Counters
                Bytes Written=524288000

```

Double check that the file created is 500MB:
```
[hdfs@london cloudera]$ hdfs dfs -ls -h /AleNegrini
Found 4 items
-rw-r--r--   1 hdfs supergroup          0 2018-03-13 09:45 /AleNegrini/_SUCCESS
-rw-r--r--   1 hdfs supergroup    166.7 M 2018-03-13 09:44 /AleNegrini/part-m-00000
-rw-r--r--   1 hdfs supergroup    166.7 M 2018-03-13 09:45 /AleNegrini/part-m-00001
-rw-r--r--   1 hdfs supergroup    166.7 M 2018-03-13 09:45 /AleNegrini/part-m-00002
```

## Distcp command

Tried to replicate the teragen file produced to jconca cluster 
```
[hdfs@london cloudera]$ hadoop distcp /AleNegrini1MB hdfs://ec2-34-245-66-209.eu-west-1.compute.amazonaws.com:8020/AleNegrini
18/03/13 10:30:39 INFO tools.DistCp: Input Options: DistCpOptions{atomicCommit=false, syncFolder=false, deleteMissing=false, ignoreFailures=false, overwrite=false, append=false, useDiff=false, useRdiff=false, fromSnapshot=null, toSnapshot=null, skipCRC=false, blocking=true, numListstatusThreads=0, maxMaps=20, mapBandwidth=100, sslConfigurationFile='null', copyStrategy='uniformsize', preserveStatus=[], preserveRawXattrs=false, atomicWorkPath=null, logPath=null, sourceFileListing=null, sourcePaths=[/AleNegrini1MB], targetPath=hdfs://ec2-34-245-66-209.eu-west-1.compute.amazonaws.com:8020/AleNegrini, targetPathExists=true, filtersFile='null'}
18/03/13 10:30:39 INFO client.RMProxy: Connecting to ResourceManager at berlin.c.sebc-labs.internal/10.142.0.3:8032
18/03/13 10:30:40 INFO tools.SimpleCopyListing: Paths (files+dirs) cnt = 5; dirCnt = 1
18/03/13 10:30:40 INFO tools.SimpleCopyListing: Build file listing completed.
18/03/13 10:30:40 INFO Configuration.deprecation: io.sort.mb is deprecated. Instead, use mapreduce.task.io.sort.mb
18/03/13 10:30:40 INFO Configuration.deprecation: io.sort.factor is deprecated. Instead, use mapreduce.task.io.sort.factor
18/03/13 10:30:40 INFO tools.DistCp: Number of paths in the copy list: 5
18/03/13 10:30:40 INFO tools.DistCp: Number of paths in the copy list: 5
18/03/13 10:30:40 INFO client.RMProxy: Connecting to ResourceManager at berlin.c.sebc-labs.internal/10.142.0.3:8032
18/03/13 10:30:40 INFO mapreduce.JobSubmitter: number of splits:4
18/03/13 10:30:40 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_1520874181129_0006
18/03/13 10:30:41 INFO impl.YarnClientImpl: Submitted application application_1520874181129_0006
18/03/13 10:30:41 INFO mapreduce.Job: The url to track the job: http://berlin.c.sebc-labs.internal:8088/proxy/application_1520874181129_0006/
18/03/13 10:30:41 INFO tools.DistCp: DistCp job-id: job_1520874181129_0006
18/03/13 10:30:41 INFO mapreduce.Job: Running job: job_1520874181129_0006
^C[hdfs@london cloudera]yarn application -list
18/03/13 10:30:55 INFO client.RMProxy: Connecting to ResourceManager at berlin.c.sebc-labs.internal/10.142.0.3:8032
Total number of applications (application-types: [] and states: [SUBMITTED, ACCEPTED, RUNNING]):2
                Application-Id      Application-Name        Application-Type          User           Queue                   State             Final-State            Progress                        Tracking-URL
application_1520874181129_0005                distcp               MAPREDUCE          hdfs      root.users.hdfs            RUNNING               UNDEFINED                 95% http://milan.c.sebc-labs.internal:42999
application_1520874181129_0006                distcp               MAPREDUCE          hdfs      root.users.hdfs           ACCEPTED               UNDEFINED                  0%                                 N/A
[hdfs@london cloudera]$ yarn application -kill application_1520874181129_0005
18/03/13 10:31:08 INFO client.RMProxy: Connecting to ResourceManager at berlin.c.sebc-labs.internal/10.142.0.3:8032
Killing application application_1520874181129_0005
18/03/13 10:31:09 INFO impl.YarnClientImpl: Killed application application_1520874181129_0005
[hdfs@london cloudera]$ yarn application -kill application_1520874181129_0006
18/03/13 10:31:19 INFO client.RMProxy: Connecting to ResourceManager at berlin.c.sebc-labs.internal/10.142.0.3:8032
Killing application application_1520874181129_0006
18/03/13 10:31:22 INFO impl.YarnClientImpl: Killed application application_1520874181129_0006
[hdfs@london cloudera]$ hadoop distcp /AleNegrini1MB hdfs://ec2-34-245-66-209.eu-west-1.compute.amazonaws.com:8020/AleNegrini
18/03/13 10:31:29 INFO tools.DistCp: Input Options: DistCpOptions{atomicCommit=false, syncFolder=false, deleteMissing=false, ignoreFailures=false, overwrite=false, append=false, useDiff=false, useRdiff=false, fromSnapshot=null, toSnapshot=null, skipCRC=false, blocking=true, numListstatusThreads=0, maxMaps=20, mapBandwidth=100, sslConfigurationFile='null', copyStrategy='uniformsize', preserveStatus=[], preserveRawXattrs=false, atomicWorkPath=null, logPath=null, sourceFileListing=null, sourcePaths=[/AleNegrini1MB], targetPath=hdfs://ec2-34-245-66-209.eu-west-1.compute.amazonaws.com:8020/AleNegrini, targetPathExists=true, filtersFile='null'}
18/03/13 10:31:29 INFO client.RMProxy: Connecting to ResourceManager at berlin.c.sebc-labs.internal/10.142.0.3:8032
18/03/13 10:31:30 INFO tools.SimpleCopyListing: Paths (files+dirs) cnt = 5; dirCnt = 1
18/03/13 10:31:30 INFO tools.SimpleCopyListing: Build file listing completed.
18/03/13 10:31:30 INFO Configuration.deprecation: io.sort.mb is deprecated. Instead, use mapreduce.task.io.sort.mb
18/03/13 10:31:30 INFO Configuration.deprecation: io.sort.factor is deprecated. Instead, use mapreduce.task.io.sort.factor
18/03/13 10:31:30 INFO tools.DistCp: Number of paths in the copy list: 5
18/03/13 10:31:30 INFO tools.DistCp: Number of paths in the copy list: 5
18/03/13 10:31:30 INFO client.RMProxy: Connecting to ResourceManager at berlin.c.sebc-labs.internal/10.142.0.3:8032
18/03/13 10:31:31 INFO mapreduce.JobSubmitter: number of splits:4
18/03/13 10:31:31 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_1520874181129_0007
18/03/13 10:31:31 INFO impl.YarnClientImpl: Submitted application application_1520874181129_0007
18/03/13 10:31:31 INFO mapreduce.Job: The url to track the job: http://berlin.c.sebc-labs.internal:8088/proxy/application_1520874181129_0007/
18/03/13 10:31:31 INFO tools.DistCp: DistCp job-id: job_1520874181129_0007
18/03/13 10:31:31 INFO mapreduce.Job: Running job: job_1520874181129_0007
18/03/13 10:31:38 INFO mapreduce.Job: Job job_1520874181129_0007 running in uber mode : false
18/03/13 10:31:38 INFO mapreduce.Job:  map 0% reduce 0%
18/03/13 10:31:46 INFO mapreduce.Job:  map 25% reduce 0%
18/03/13 10:31:49 INFO mapreduce.Job:  map 50% reduce 0%
18/03/13 10:31:52 INFO mapreduce.Job:  map 100% reduce 0%
18/03/13 10:40:53 INFO mapreduce.Job: Task Id : attempt_1520874181129_0007_m_000003_0, Status : FAILED
Error: java.io.IOException: File copy failed: hdfs://amsterdam.c.sebc-labs.internal:8020/AleNegrini1MB/part-m-00002 --> hdfs://ec2-34-245-66-209.eu-west-1.compute.amazonaws.com:8020/AleNegrini/AleNegrini1MB/part-m-00002
        at org.apache.hadoop.tools.mapred.CopyMapper.copyFileWithRetry(CopyMapper.java:284)
        at org.apache.hadoop.tools.mapred.CopyMapper.map(CopyMapper.java:252)
        at org.apache.hadoop.tools.mapred.CopyMapper.map(CopyMapper.java:50)
        at org.apache.hadoop.mapreduce.Mapper.run(Mapper.java:145)
        at org.apache.hadoop.mapred.MapTask.runNewMapper(MapTask.java:787)
        at org.apache.hadoop.mapred.MapTask.run(MapTask.java:341)
        at org.apache.hadoop.mapred.YarnChild$2.run(YarnChild.java:164)
        at java.security.AccessController.doPrivileged(Native Method)
        at javax.security.auth.Subject.doAs(Subject.java:415)
        at org.apache.hadoop.security.UserGroupInformation.doAs(UserGroupInformation.java:1912)
        at org.apache.hadoop.mapred.YarnChild.main(YarnChild.java:158)
Caused by: java.io.IOException: Couldn't run retriable-command: Copying hdfs://amsterdam.c.sebc-labs.internal:8020/AleNegrini1MB/part-m-00002 to hdfs://ec2-34-245-66-209.eu-west-1.compute.amazonaws.com:8020/AleNegrini/AleNegrini1MB/part-m-00002
        at org.apache.hadoop.tools.util.RetriableCommand.execute(RetriableCommand.java:101)
        at org.apache.hadoop.tools.mapred.CopyMapper.copyFileWithRetry(CopyMapper.java:280)
        ... 10 more
Caused by: org.apache.hadoop.ipc.RemoteException(java.io.IOException): File /AleNegrini/.distcp.tmp.attempt_1520874181129_0007_m_000003_0 could only be replicated to 0 nodes instead of minReplication (=1).  There are 3 datanode(s) running and 3 node(s) are excluded in this operation.
        at org.apache.hadoop.hdfs.server.blockmanagement.BlockManager.chooseTarget4NewBlock(BlockManager.java:1626)
        at org.apache.hadoop.hdfs.server.namenode.FSNamesystem.getAdditionalBlock(FSNamesystem.java:3351)
        at org.apache.hadoop.hdfs.server.namenode.NameNodeRpcServer.addBlock(NameNodeRpcServer.java:683)
        at org.apache.hadoop.hdfs.server.namenode.AuthorizationProviderProxyClientProtocol.addBlock(AuthorizationProviderProxyClientProtocol.java:214)
        at org.apache.hadoop.hdfs.protocolPB.ClientNamenodeProtocolServerSideTranslatorPB.addBlock(ClientNamenodeProtocolServerSideTranslatorPB.java:495)
        at org.apache.hadoop.hdfs.protocol.proto.ClientNamenodeProtocolProtos$ClientNamenodeProtocol$2.callBlockingMethod(ClientNamenodeProtocolProtos.java)
        at org.apache.hadoop.ipc.ProtobufRpcEngine$Server$ProtoBufRpcInvoker.call(ProtobufRpcEngine.java:617)
        at org.apache.hadoop.ipc.RPC$Server.call(RPC.java:1073)
        at org.apache.hadoop.ipc.Server$Handler$1.run(Server.java:2141)
        at org.apache.hadoop.ipc.Server$Handler$1.run(Server.java:2137)
        at java.security.AccessController.doPrivileged(Native Method)
        at javax.security.auth.Subject.doAs(Subject.java:415)
        at org.apache.hadoop.security.UserGroupInformation.doAs(UserGroupInformation.java:1912)
        at org.apache.hadoop.ipc.Server$Handler.run(Server.java:2135)

        at org.apache.hadoop.ipc.Client.call(Client.java:1502)
        at org.apache.hadoop.ipc.Client.call(Client.java:1439)
        at org.apache.hadoop.ipc.ProtobufRpcEngine$Invoker.invoke(ProtobufRpcEngine.java:230)
        at com.sun.proxy.$Proxy15.addBlock(Unknown Source)
        at org.apache.hadoop.hdfs.protocolPB.ClientNamenodeProtocolTranslatorPB.addBlock(ClientNamenodeProtocolTranslatorPB.java:413)
        at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:57)
        at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
        at java.lang.reflect.Method.invoke(Method.java:606)
        at org.apache.hadoop.io.retry.RetryInvocationHandler.invokeMethod(RetryInvocationHandler.java:256)
        at org.apache.hadoop.io.retry.RetryInvocationHandler.invoke(RetryInvocationHandler.java:104)
        at com.sun.proxy.$Proxy16.addBlock(Unknown Source)
        at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.locateFollowingBlock(DFSOutputStream.java:1811)
        at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.nextBlockOutputStream(DFSOutputStream.java:1607)
        at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.run(DFSOutputStream.java:771)

18/03/13 10:40:54 INFO mapreduce.Job:  map 75% reduce 0%
18/03/13 10:40:56 INFO mapreduce.Job: Task Id : attempt_1520874181129_0007_m_000002_0, Status : FAILED
Error: java.io.IOException: File copy failed: hdfs://amsterdam.c.sebc-labs.internal:8020/AleNegrini1MB/part-m-00001 --> hdfs://ec2-34-245-66-209.eu-west-1.compute.amazonaws.com:8020/AleNegrini/AleNegrini1MB/part-m-00001
        at org.apache.hadoop.tools.mapred.CopyMapper.copyFileWithRetry(CopyMapper.java:284)
        at org.apache.hadoop.tools.mapred.CopyMapper.map(CopyMapper.java:252)
        at org.apache.hadoop.tools.mapred.CopyMapper.map(CopyMapper.java:50)
        at org.apache.hadoop.mapreduce.Mapper.run(Mapper.java:145)
        at org.apache.hadoop.mapred.MapTask.runNewMapper(MapTask.java:787)
        at org.apache.hadoop.mapred.MapTask.run(MapTask.java:341)
        at org.apache.hadoop.mapred.YarnChild$2.run(YarnChild.java:164)
        at java.security.AccessController.doPrivileged(Native Method)
        at javax.security.auth.Subject.doAs(Subject.java:415)
        at org.apache.hadoop.security.UserGroupInformation.doAs(UserGroupInformation.java:1912)
        at org.apache.hadoop.mapred.YarnChild.main(YarnChild.java:158)
Caused by: java.io.IOException: Couldn't run retriable-command: Copying hdfs://amsterdam.c.sebc-labs.internal:8020/AleNegrini1MB/part-m-00001 to hdfs://ec2-34-245-66-209.eu-west-1.compute.amazonaws.com:8020/AleNegrini/AleNegrini1MB/part-m-00001
        at org.apache.hadoop.tools.util.RetriableCommand.execute(RetriableCommand.java:101)
        at org.apache.hadoop.tools.mapred.CopyMapper.copyFileWithRetry(CopyMapper.java:280)
        ... 10 more
Caused by: org.apache.hadoop.ipc.RemoteException(java.io.IOException): File /AleNegrini/.distcp.tmp.attempt_1520874181129_0007_m_000002_0 could only be replicated to 0 nodes instead of minReplication (=1).  There are 3 datanode(s) running and 3 node(s) are excluded in this operation.
        at org.apache.hadoop.hdfs.server.blockmanagement.BlockManager.chooseTarget4NewBlock(BlockManager.java:1626)
        at org.apache.hadoop.hdfs.server.namenode.FSNamesystem.getAdditionalBlock(FSNamesystem.java:3351)
        at org.apache.hadoop.hdfs.server.namenode.NameNodeRpcServer.addBlock(NameNodeRpcServer.java:683)
        at org.apache.hadoop.hdfs.server.namenode.AuthorizationProviderProxyClientProtocol.addBlock(AuthorizationProviderProxyClientProtocol.java:214)
        at org.apache.hadoop.hdfs.protocolPB.ClientNamenodeProtocolServerSideTranslatorPB.addBlock(ClientNamenodeProtocolServerSideTranslatorPB.java:495)
        at org.apache.hadoop.hdfs.protocol.proto.ClientNamenodeProtocolProtos$ClientNamenodeProtocol$2.callBlockingMethod(ClientNamenodeProtocolProtos.java)
        at org.apache.hadoop.ipc.ProtobufRpcEngine$Server$ProtoBufRpcInvoker.call(ProtobufRpcEngine.java:617)
        at org.apache.hadoop.ipc.RPC$Server.call(RPC.java:1073)
        at org.apache.hadoop.ipc.Server$Handler$1.run(Server.java:2141)
        at org.apache.hadoop.ipc.Server$Handler$1.run(Server.java:2137)
        at java.security.AccessController.doPrivileged(Native Method)
        at javax.security.auth.Subject.doAs(Subject.java:415)
        at org.apache.hadoop.security.UserGroupInformation.doAs(UserGroupInformation.java:1912)
        at org.apache.hadoop.ipc.Server$Handler.run(Server.java:2135)

        at org.apache.hadoop.ipc.Client.call(Client.java:1502)
        at org.apache.hadoop.ipc.Client.call(Client.java:1439)
        at org.apache.hadoop.ipc.ProtobufRpcEngine$Invoker.invoke(ProtobufRpcEngine.java:230)
        at com.sun.proxy.$Proxy15.addBlock(Unknown Source)
        at org.apache.hadoop.hdfs.protocolPB.ClientNamenodeProtocolTranslatorPB.addBlock(ClientNamenodeProtocolTranslatorPB.java:413)
        at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:57)
        at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
        at java.lang.reflect.Method.invoke(Method.java:606)
        at org.apache.hadoop.io.retry.RetryInvocationHandler.invokeMethod(RetryInvocationHandler.java:256)
        at org.apache.hadoop.io.retry.RetryInvocationHandler.invoke(RetryInvocationHandler.java:104)
        at com.sun.proxy.$Proxy16.addBlock(Unknown Source)
        at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.locateFollowingBlock(DFSOutputStream.java:1811)
        at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.nextBlockOutputStream(DFSOutputStream.java:1607)
        at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.run(DFSOutputStream.java:771)

18/03/13 10:40:57 INFO mapreduce.Job:  map 50% reduce 0%
18/03/13 10:40:57 INFO mapreduce.Job: Task Id : attempt_1520874181129_0007_m_000001_0, Status : FAILED
Error: java.io.IOException: File copy failed: hdfs://amsterdam.c.sebc-labs.internal:8020/AleNegrini1MB/part-m-00000 --> hdfs://ec2-34-245-66-209.eu-west-1.compute.amazonaws.com:8020/AleNegrini/AleNegrini1MB/part-m-00000
        at org.apache.hadoop.tools.mapred.CopyMapper.copyFileWithRetry(CopyMapper.java:284)
        at org.apache.hadoop.tools.mapred.CopyMapper.map(CopyMapper.java:252)
        at org.apache.hadoop.tools.mapred.CopyMapper.map(CopyMapper.java:50)
        at org.apache.hadoop.mapreduce.Mapper.run(Mapper.java:145)
        at org.apache.hadoop.mapred.MapTask.runNewMapper(MapTask.java:787)
        at org.apache.hadoop.mapred.MapTask.run(MapTask.java:341)
        at org.apache.hadoop.mapred.YarnChild$2.run(YarnChild.java:164)
        at java.security.AccessController.doPrivileged(Native Method)
        at javax.security.auth.Subject.doAs(Subject.java:415)
        at org.apache.hadoop.security.UserGroupInformation.doAs(UserGroupInformation.java:1912)
        at org.apache.hadoop.mapred.YarnChild.main(YarnChild.java:158)
```
Since the datanodes are not listening on the public interface, we cannot transfer data between two clusters. 

Let's try to transfer data within the same cluster: 
```
[hdfs@london cloudera]$ hadoop distcp /AleNegrini /user/AleNegrini_copied
18/03/13 10:52:02 INFO tools.DistCp: Input Options: DistCpOptions{atomicCommit=false, syncFolder=false, deleteMissing=false, ignoreFailures=false, overwrite=false, append=false, useDiff=false, useRdiff=false, fromSnapshot=null, toSnapshot=null, skipCRC=false, blocking=true, numListstatusThreads=0, maxMaps=20, mapBandwidth=100, sslConfigurationFile='null', copyStrategy='uniformsize', preserveStatus=[], preserveRawXattrs=false, atomicWorkPath=null, logPath=null, sourceFileListing=null, sourcePaths=[/AleNegrini], targetPath=/user/AleNegrini_copied, targetPathExists=false, filtersFile='null'}
18/03/13 10:52:02 INFO client.RMProxy: Connecting to ResourceManager at berlin.c.sebc-labs.internal/10.142.0.3:8032
18/03/13 10:52:03 INFO tools.SimpleCopyListing: Paths (files+dirs) cnt = 5; dirCnt = 1
18/03/13 10:52:03 INFO tools.SimpleCopyListing: Build file listing completed.
18/03/13 10:52:03 INFO Configuration.deprecation: io.sort.mb is deprecated. Instead, use mapreduce.task.io.sort.mb
18/03/13 10:52:03 INFO Configuration.deprecation: io.sort.factor is deprecated. Instead, use mapreduce.task.io.sort.factor
18/03/13 10:52:03 INFO tools.DistCp: Number of paths in the copy list: 5
18/03/13 10:52:03 INFO tools.DistCp: Number of paths in the copy list: 5
18/03/13 10:52:03 INFO client.RMProxy: Connecting to ResourceManager at berlin.c.sebc-labs.internal/10.142.0.3:8032
18/03/13 10:52:03 INFO mapreduce.JobSubmitter: number of splits:4
18/03/13 10:52:04 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_1520874181129_0009
18/03/13 10:52:04 INFO impl.YarnClientImpl: Submitted application application_1520874181129_0009
18/03/13 10:52:04 INFO mapreduce.Job: The url to track the job: http://berlin.c.sebc-labs.internal:8088/proxy/application_1520874181129_0009/
18/03/13 10:52:04 INFO tools.DistCp: DistCp job-id: job_1520874181129_0009
18/03/13 10:52:04 INFO mapreduce.Job: Running job: job_1520874181129_0009
18/03/13 10:52:10 INFO mapreduce.Job: Job job_1520874181129_0009 running in uber mode : false
18/03/13 10:52:10 INFO mapreduce.Job:  map 0% reduce 0%
18/03/13 10:52:20 INFO mapreduce.Job:  map 25% reduce 0%
18/03/13 10:52:21 INFO mapreduce.Job:  map 75% reduce 0%
18/03/13 10:52:23 INFO mapreduce.Job:  map 100% reduce 0%
18/03/13 10:52:24 INFO mapreduce.Job: Job job_1520874181129_0009 completed successfully
18/03/13 10:52:24 INFO mapreduce.Job: Counters: 33
        File System Counters
                FILE: Number of bytes read=0
                FILE: Number of bytes written=505144
                FILE: Number of read operations=0
                FILE: Number of large read operations=0
                FILE: Number of write operations=0
                HDFS: Number of bytes read=524290210
                HDFS: Number of bytes written=524288000
                HDFS: Number of read operations=75
                HDFS: Number of large read operations=0
                HDFS: Number of write operations=17
        Job Counters
                Launched map tasks=4
                Other local map tasks=4
                Total time spent by all maps in occupied slots (ms)=35346
                Total time spent by all reduces in occupied slots (ms)=0
                Total time spent by all map tasks (ms)=35346
                Total vcore-seconds taken by all map tasks=35346
                Total megabyte-seconds taken by all map tasks=36194304
        Map-Reduce Framework
                Map input records=5
                Map output records=0
                Input split bytes=460
                Spilled Records=0
                Failed Shuffles=0
                Merged Map outputs=0
                GC time elapsed (ms)=439
                CPU time spent (ms)=13200
                Physical memory (bytes) snapshot=1044795392
                Virtual memory (bytes) snapshot=6284075008
                Total committed heap usage (bytes)=1347420160
        File Input Format Counters
                Bytes Read=1750
        File Output Format Counters
                Bytes Written=0
        org.apache.hadoop.tools.mapred.CopyMapper$Counter
                BYTESCOPIED=524288000
                BYTESEXPECTED=524288000
                COPY=5
```
Double check the copied files
```
[hdfs@london cloudera]$ hdfs dfs -ls /user/AleNegrini_copied
Found 4 items
-rw-r--r--   3 hdfs supergroup          0 2018-03-13 10:52 /user/AleNegrini_copied/_SUCCESS
-rw-r--r--   3 hdfs supergroup  174762700 2018-03-13 10:52 /user/AleNegrini_copied/part-m-00000
-rw-r--r--   3 hdfs supergroup  174762700 2018-03-13 10:52 /user/AleNegrini_copied/part-m-00001
-rw-r--r--   3 hdfs supergroup  174762600 2018-03-13 10:52 /user/AleNegrini_copied/part-m-00002
```

## Checking folders

Since the teragen was launched with REP=1 option, when I launched __fsck__ command I got: 
```
[hdfs@london cloudera]$ hdfs fsck /AleNegrini -files -blocks
Connecting to namenode via http://amsterdam.c.sebc-labs.internal:50070
FSCK started by hdfs (auth:SIMPLE) from /10.142.0.5 for path /AleNegrini at Tue Mar 13 10:55:57 UTC 2018
/AleNegrini <dir>
/AleNegrini/_SUCCESS 0 bytes, 0 block(s):  OK

/AleNegrini/part-m-00000 174762700 bytes, 2 block(s):  OK
0. BP-1004015303-10.142.0.2-1520874104410:blk_1073743509_2685 len=134217728 Live_repl=1
1. BP-1004015303-10.142.0.2-1520874104410:blk_1073743510_2686 len=40544972 Live_repl=1

/AleNegrini/part-m-00001 174762700 bytes, 2 block(s):  OK
0. BP-1004015303-10.142.0.2-1520874104410:blk_1073743512_2688 len=134217728 Live_repl=1
1. BP-1004015303-10.142.0.2-1520874104410:blk_1073743516_2692 len=40544972 Live_repl=1

/AleNegrini/part-m-00002 174762600 bytes, 2 block(s):  OK
0. BP-1004015303-10.142.0.2-1520874104410:blk_1073743513_2689 len=134217728 Live_repl=1
1. BP-1004015303-10.142.0.2-1520874104410:blk_1073743515_2691 len=40544872 Live_repl=1

Status: HEALTHY
 Total size:    524288000 B
 Total dirs:    1
 Total files:   4
 Total symlinks:                0
 Total blocks (validated):      6 (avg. block size 87381333 B)
 Minimally replicated blocks:   6 (100.0 %)
 Over-replicated blocks:        0 (0.0 %)
 Under-replicated blocks:       0 (0.0 %)
 Mis-replicated blocks:         0 (0.0 %)
 Default replication factor:    3
 Average block replication:     1.0
 Corrupt blocks:                0
 Missing replicas:              0 (0.0 %)
 Number of data-nodes:          3
 Number of racks:               1
FSCK ended at Tue Mar 13 10:55:57 UTC 2018 in 1 milliseconds
```

If instead, I try to check the copied files, I got a replication factor of 3: 
```
[hdfs@london cloudera]$ hdfs fsck /user/AleNegrini_copied -files -blocks
Connecting to namenode via http://amsterdam.c.sebc-labs.internal:50070
FSCK started by hdfs (auth:SIMPLE) from /10.142.0.5 for path /user/AleNegrini_copied at Tue Mar 13 10:55:40 UTC 2018
/user/AleNegrini_copied <dir>
/user/AleNegrini_copied/_SUCCESS 0 bytes, 0 block(s):  OK

/user/AleNegrini_copied/part-m-00000 174762700 bytes, 2 block(s):  OK
0. BP-1004015303-10.142.0.2-1520874104410:blk_1073743960_3136 len=134217728 Live_repl=3
1. BP-1004015303-10.142.0.2-1520874104410:blk_1073743961_3137 len=40544972 Live_repl=3

/user/AleNegrini_copied/part-m-00001 174762700 bytes, 2 block(s):  OK
0. BP-1004015303-10.142.0.2-1520874104410:blk_1073743955_3131 len=134217728 Live_repl=3
1. BP-1004015303-10.142.0.2-1520874104410:blk_1073743958_3134 len=40544972 Live_repl=3

/user/AleNegrini_copied/part-m-00002 174762600 bytes, 2 block(s):  OK
0. BP-1004015303-10.142.0.2-1520874104410:blk_1073743954_3130 len=134217728 Live_repl=3
1. BP-1004015303-10.142.0.2-1520874104410:blk_1073743957_3133 len=40544872 Live_repl=3

Status: HEALTHY
 Total size:    524288000 B
 Total dirs:    1
 Total files:   4
 Total symlinks:                0
 Total blocks (validated):      6 (avg. block size 87381333 B)
 Minimally replicated blocks:   6 (100.0 %)
 Over-replicated blocks:        0 (0.0 %)
 Under-replicated blocks:       0 (0.0 %)
 Mis-replicated blocks:         0 (0.0 %)
 Default replication factor:    3
 Average block replication:     3.0
 Corrupt blocks:                0
 Missing replicas:              0 (0.0 %)
 Number of data-nodes:          3
 Number of racks:               1
FSCK ended at Tue Mar 13 10:55:40 UTC 2018 in 4 milliseconds
```
