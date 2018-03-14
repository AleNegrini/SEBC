# Treasure hunt

## What is ubertask optimization?
Uberstask optimization is a YARN feature that allows to runs "sufficiently small" jobs sequentially within a single JVM. 
By default it is disabled; by typing on the top right corner of the CM "uberstask" you get some configurations.
First thing is to enable it in the YARN configuration tab. 
Via search bar you can also get access to ubertask configuration settings, like:
* mapreduce.job.ubertask.maxmaps
* mapreduce.job.ubertask.maxreduces
* mapreduce.job.ubertask.maxbytes 
that define what "small" mean. 

## Where in CM is the Kerberos Security Realm value displayed?
Administration -> Settings -> Kerberos -> Kerberos Security Realm. 
The default one is HADOOP.COM

## Which CDH service(s) host a property for enabling Kerberos authentication
By tiping on the search bar "Kerberos Principal", you can get all the services hosting a property for enabling Kerberos authentication. In my case:
* Hive
* Zookeeper
* Hue
* Oozie
* HDFS
* YARN

## How do you upgrade the CM agents?

## Give the tsquery statement used to chart Hue's CPU utilization
SELECT cpu_system_rate + cpu_user_rate WHERE entityName = "hue-HUE_SERVER-d13cf07e51c6ba1367cb6597c9a8deb6" AND category = ROLE