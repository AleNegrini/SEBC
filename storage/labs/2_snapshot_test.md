# Snapshot feature

## HDFS folder creation 
Create __precious__ folder in HDFS:
```
[root@milan cloudera]# sudo su hdfs
[hdfs@milan cloudera]$ hdfs dfs -mkdir /precious
[hdfs@milan cloudera]$ hdfs dfs -ls /
Found 5 items
drwxr-xr-x   - hdfs supergroup          0 2018-03-13 09:45 /AleNegrini
drwxrwxrwx   - hdfs supergroup          0 2018-03-13 10:37 /jconca
drwxr-xr-x   - hdfs supergroup          0 2018-03-13 12:07 /precious
drwxrwxrwt   - hdfs supergroup          0 2018-03-12 17:04 /tmp
drwxr-xr-x   - hdfs supergroup          0 2018-03-13 11:04 /user
```

Add the ZIP folder course to HDFS folder
```
[hdfs@milan cloudera]$ cd /tmp/
[hdfs@milan tmp]$ hdfs dfs -put SEBC.zip /precious
[hdfs@milan tmp]$ hdfs dfs -ls /precious
Found 1 items
-rw-r--r--   3 hdfs supergroup    1385720 2018-03-13 12:10 /precious/SEBC.zip
```

## Snapshot enablement

I enabled the snapshot for __precious__ from Cloudera Manager UI, following these following steps:
```
HDFS -> File Browser -> select 'precious' -> on the arrow in the top right corner, click "Enable Snapshot"
```

## Take Snapshot 
I took the snapshot from the Cloudera Manager UI, following these following steps:
```
HDFS -> File Browser -> select 'precious' -> on the arrow in the top right corner, click "Take Snapshot" -> give it "sebc-hdfs-test" name
```

## Delete directory/file
```
[hdfs@milan tmp]$ hdfs dfs -rm -r /precious
rm: Failed to move to trash: hdfs://amsterdam.c.sebc-labs.internal:8020/precious: The directory /precious cannot be deleted since /precious is snapshottable and already has snapshots
```
A snapshottable folder cannot be deleted

Let's delete the file contained in:
```
[hdfs@milan tmp]$ hdfs dfs -rm -r /precious/SEBC.zip
18/03/13 12:29:32 INFO fs.TrashPolicyDefault: Moved: 'hdfs://amsterdam.c.sebc-labs.internal:8020/precious/SEBC.zip' to trash at: hdfs://amsterdam.c.sebc-labs.internal:8020/user/hdfs/.Trash/Current/precious/SEBC.zip
[hdfs@milan tmp]$ hdfs dfs -ls /precious 
(empty set as expected)
[hdfs@milan tmp]$
```

## Restore from a database
I restored the snapshot from the Cloudera Manager UI:
```
HDFS -> File Browser -> select 'precious' -> on the arrow in the top right corner, click "Restore Directory From Snapshot " -> select the "sebc-hdfs-test" snapshot -> selected "copy" option for the restoring -> Click on "restore" button
```
Double check that the file has been correctly restored
```
[hdfs@milan tmp]$ hdfs dfs -ls /precious
Found 1 items
-rw-r--r--   3 hdfs supergroup    1385720 2018-03-13 12:35 /precious/SEBC.zip
[hdfs@milan tmp]$
```

Please note that the time at which file has been written is different from the previous one (before the deletion)
