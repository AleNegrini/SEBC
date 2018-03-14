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
By tiping on the search bar "Kerberos Principal", you can get all the services hosting a property for enabling Kerberos authentication. In my cluster are:
* Hive
* Zookeeper
* Hue
* Oozie
* HDFS
* YARN

However in general: 
  - Flume 
  - HBase 
  - HCatalog 
  - Hive 
  - HttpFS 
  - Hue 
  - Impala 
  - Llama 
  - Oozie 
  - Solr 
  - Spark 
  - Sqoop 
  - ZooKeeper

## How do you upgrade the CM agents?
You need first to upgrade the cloudera manager Server. Once the CM server is upgrade and restarted a wizard pops up to upgrade the cloudera manager agents and optionally the JDK

## Give the tsquery statement used to chart Hue's CPU utilization
SELECT cpu_system_rate + cpu_user_rate WHERE entityName = "hue-HUE_SERVER-d13cf07e51c6ba1367cb6597c9a8deb6" AND category = ROLE

## Name all the roles that make up the Hive service
* Gateway
* Hive Metastore Server
* HiveServer2
* WebHcat Server 

## What steps must be completed before integrating Cloudera Manager with Kerberos
* Install `openldap-clients` on the Cloudera Manager Server host. Install `krb5-workstation` `krb5-libs` on ALL hosts
* Install `MIT KDC` or use the `Active Directory KDC`
* Create Kerberos Principal for the Cloudera Manager Server
* Configure the KDC to allow renewable tickets with non-zero ticket lifetimes. Active Directory KDC allows it by default
* Start the Wizard for Kerberos Integration