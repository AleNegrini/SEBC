## User HDFS directories

On the inspecting host window during the CM installation everything is fine. 
Also the connection to the databases were fine. 

Commands launched on a datanode:
* Create user directories: 
```
[root@london ~]# su hdfs
[hdfs@london root]$ hdfs dfs -ls /
Found 2 items
drwxrwxrwt   - hdfs supergroup          0 2018-03-16 09:34 /tmp
drwxr-xr-x   - hdfs supergroup          0 2018-03-16 09:34 /user
[hdfs@london root]$ hdfs dfs -mkdir /user/hilary
[hdfs@london root]$ hdfs dfs -mkdir /user/anupam
[hdfs@london root]$ hdfs dfs -chown hilary /user/hilary
[hdfs@london root]$ hdfs dfs -chown anupam /user/anupam
[hdfs@london root]$ hdfs dfs -ls /user
Found 4 items
drwxr-xr-x   - anupam supergroup          0 2018-03-16 09:35 /user/anupam
drwxr-xr-x   - hilary supergroup          0 2018-03-16 09:34 /user/hilary
drwxrwxrwx   - mapred hadoop              0 2018-03-16 09:34 /user/history
drwxrwxr-t   - hive   hive                0 2018-03-16 09:35 /user/hive
```

## API call

```
[hdfs@london root]$ url -u admin:admin 'http://104.196.177.232:7180/api/v14/hosts'
{
  "items" : [ {
    "hostId" : "ddc88b12-0c4e-4642-932d-2b28a10f2bd7",
    "ipAddress" : "10.142.0.2",
    "hostname" : "amsterdam.c.sebc-pre-challenges.internal",
    "rackId" : "/default",
    "hostUrl" : "http://berlin.c.sebc-pre-challenges.internal:7180/cmf/hostRedirect/ddc88b12-0c4e-4642-932d-2b28a10f2bd7",
    "maintenanceMode" : false,
    "maintenanceOwners" : [ ],
    "commissionState" : "COMMISSIONED",
    "numCores" : 2,
    "numPhysicalCores" : 1,
    "totalPhysMemBytes" : 13487558656
  }, {
    "hostId" : "57f4eea4-2e97-4245-b1c9-61654102e2e9",
    "ipAddress" : "10.142.0.6",
    "hostname" : "berlin.c.sebc-pre-challenges.internal",
    "rackId" : "/default",
    "hostUrl" : "http://berlin.c.sebc-pre-challenges.internal:7180/cmf/hostRedirect/57f4eea4-2e97-4245-b1c9-61654102e2e9",
    "maintenanceMode" : false,
    "maintenanceOwners" : [ ],
    "commissionState" : "COMMISSIONED",
    "numCores" : 2,
    "numPhysicalCores" : 1,
    "totalPhysMemBytes" : 13487558656
  }, {
    "hostId" : "6699fe12-f4b1-4c38-9c5e-7ef800833ed4",
    "ipAddress" : "10.142.0.5",
    "hostname" : "london.c.sebc-pre-challenges.internal",
    "rackId" : "/default",
    "hostUrl" : "http://berlin.c.sebc-pre-challenges.internal:7180/cmf/hostRedirect/6699fe12-f4b1-4c38-9c5e-7ef800833ed4",
    "maintenanceMode" : false,
    "maintenanceOwners" : [ ],
    "commissionState" : "COMMISSIONED",
    "numCores" : 2,
    "numPhysicalCores" : 1,
    "totalPhysMemBytes" : 13487558656
  }, {
    "hostId" : "01c727e0-e09c-4eb8-9e9e-fac84d884306",
    "ipAddress" : "10.142.0.3",
    "hostname" : "milan.c.sebc-pre-challenges.internal",
    "rackId" : "/default",
    "hostUrl" : "http://berlin.c.sebc-pre-challenges.internal:7180/cmf/hostRedirect/01c727e0-e09c-4eb8-9e9e-fac84d884306",
    "maintenanceMode" : false,
    "maintenanceOwners" : [ ],
    "commissionState" : "COMMISSIONED",
    "numCores" : 2,
    "numPhysicalCores" : 1,
    "totalPhysMemBytes" : 13487558656
  }, {
    "hostId" : "63754fbe-6c5d-4b15-992a-84639295f85a",
    "ipAddress" : "10.142.0.4",
    "hostname" : "paris.c.sebc-pre-challenges.internal",
    "rackId" : "/default",
    "hostUrl" : "http://berlin.c.sebc-pre-challenges.internal:7180/cmf/hostRedirect/63754fbe-6c5d-4b15-992a-84639295f85a",
    "maintenanceMode" : false,
    "maintenanceOwners" : [ ],
    "commissionState" : "COMMISSIONED",
    "numCores" : 2,
    "numPhysicalCores" : 1,
    "totalPhysMemBytes" : 13487558656
  } ]
}

[hdfs@london root]$ curl -u admin:admin 'http://104.196.177.232:7180/api/v8/clusters'
{
  "items" : [ {
    "name" : "cluster",
    "displayName" : "AleNegrini",
    "version" : "CDH5",
    "fullVersion" : "5.13.2",
    "maintenanceMode" : false,
    "maintenanceOwners" : [ ]
  } ]
}

[hdfs@london root]$ curl -u admin:admin 'http://104.196.177.232:7180/api/v8/cluters/AleNegrini/services'
{
  "items" : [ {
    "name" : "hive",
    "type" : "HIVE",
    "clusterRef" : {
      "clusterName" : "cluster"
    },
    "serviceUrl" : "http://berlin.c.sebc-pre-challenges.internal:7180/cmf/serviceRedirect/hive",
    "serviceState" : "STARTED",
    "healthSummary" : "GOOD",
    "healthChecks" : [ {
      "name" : "HIVE_HIVEMETASTORES_HEALTHY",
      "summary" : "GOOD"
    }, {
      "name" : "HIVE_HIVESERVER2S_HEALTHY",
      "summary" : "GOOD"
    } ],
    "configStalenessStatus" : "FRESH",
    "clientConfigStalenessStatus" : "FRESH",
    "maintenanceMode" : false,
    "maintenanceOwners" : [ ],
    "displayName" : "Hive"
  }, {
    "name" : "zookeeper",
    "type" : "ZOOKEEPER",
    "clusterRef" : {
      "clusterName" : "cluster"
    },
    "serviceUrl" : "http://berlin.c.sebc-pre-challenges.internal:7180/cmf/serviceRedirect/zookeeper",
    "serviceState" : "STARTED",
    "healthSummary" : "GOOD",
    "healthChecks" : [ {
      "name" : "ZOOKEEPER_CANARY_HEALTH",
      "summary" : "GOOD"
    }, {
      "name" : "ZOOKEEPER_SERVERS_HEALTHY",
      "summary" : "GOOD"
    } ],
    "configStalenessStatus" : "FRESH",
    "clientConfigStalenessStatus" : "FRESH",
    "maintenanceMode" : false,
    "maintenanceOwners" : [ ],
    "displayName" : "ZooKeeper"
  }, {
    "name" : "hue",
    "type" : "HUE",
    "clusterRef" : {
      "clusterName" : "cluster"
    },
    "serviceUrl" : "http://berlin.c.sebc-pre-challenges.internal:7180/cmf/serviceRedirect/hue",
    "serviceState" : "STARTED",
    "healthSummary" : "GOOD",
    "healthChecks" : [ {
      "name" : "HUE_HUE_SERVERS_HEALTHY",
      "summary" : "GOOD"
    }, {
      "name" : "HUE_LOAD_BALANCER_HEALTHY",
      "summary" : "GOOD"
    } ],
    "configStalenessStatus" : "FRESH",
    "clientConfigStalenessStatus" : "FRESH",
    "maintenanceMode" : false,
    "maintenanceOwners" : [ ],
    "displayName" : "Hue"
  }, {
    "name" : "oozie",
    "type" : "OOZIE",
    "clusterRef" : {
      "clusterName" : "cluster"
    },
    "serviceUrl" : "http://berlin.c.sebc-pre-challenges.internal:7180/cmf/serviceRedirect/oozie",
    "serviceState" : "STARTED",
    "healthSummary" : "GOOD",
    "healthChecks" : [ {
      "name" : "OOZIE_OOZIE_SERVERS_HEALTHY",
      "summary" : "GOOD"
    } ],
    "configStalenessStatus" : "FRESH",
    "clientConfigStalenessStatus" : "FRESH",
    "maintenanceMode" : false,
    "maintenanceOwners" : [ ],
    "displayName" : "Oozie"
  }, {
    "name" : "yarn",
    "type" : "YARN",
    "clusterRef" : {
      "clusterName" : "cluster"
    },
    "serviceUrl" : "http://berlin.c.sebc-pre-challenges.internal:7180/cmf/serviceRedirect/yarn",
    "serviceState" : "STARTED",
    "healthSummary" : "GOOD",
    "healthChecks" : [ {
      "name" : "YARN_JOBHISTORY_HEALTH",
      "summary" : "GOOD"
    }, {
      "name" : "YARN_NODE_MANAGERS_HEALTHY",
      "summary" : "GOOD"
    }, {
      "name" : "YARN_RESOURCEMANAGERS_HEALTH",
      "summary" : "GOOD"
    }, {
      "name" : "YARN_USAGE_AGGREGATION_HEALTH",
      "summary" : "DISABLED"
    } ],
    "configStalenessStatus" : "FRESH",
    "clientConfigStalenessStatus" : "FRESH",
    "maintenanceMode" : false,
    "maintenanceOwners" : [ ],
    "displayName" : "YARN (MR2 Included)"
  }, {
    "name" : "hdfs",
    "type" : "HDFS",
    "clusterRef" : {
      "clusterName" : "cluster"
    },
    "serviceUrl" : "http://berlin.c.sebc-pre-challenges.internal:7180/cmf/serviceRedirect/hdfs",
    "serviceState" : "STARTED",
    "healthSummary" : "GOOD",
    "healthChecks" : [ {
      "name" : "HDFS_BLOCKS_WITH_CORRUPT_REPLICAS",
      "summary" : "GOOD"
    }, {
      "name" : "HDFS_CANARY_HEALTH",
      "summary" : "GOOD"
    }, {
      "name" : "HDFS_DATA_NODES_HEALTHY",
      "summary" : "GOOD"
    }, {
      "name" : "HDFS_FREE_SPACE_REMAINING",
      "summary" : "GOOD"
    }, {
      "name" : "HDFS_HA_NAMENODE_HEALTH",
      "summary" : "GOOD"
    }, {
      "name" : "HDFS_MISSING_BLOCKS",
      "summary" : "GOOD"
    }, {
      "name" : "HDFS_UNDER_REPLICATED_BLOCKS",
      "summary" : "GOOD"
    } ],
    "configStalenessStatus" : "FRESH",
    "clientConfigStalenessStatus" : "FRESH",
    "maintenanceMode" : false,
    "maintenanceOwners" : [ ],
    "displayName" : "HDFS"
  } ]
}
```