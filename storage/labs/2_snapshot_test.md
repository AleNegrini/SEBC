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

