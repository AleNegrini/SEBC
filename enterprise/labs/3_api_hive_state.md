```
[root@amsterdam cloudera-scm-server]# curl u AleNegrini:cloudera 'http://localhost:7180/api/version'                                          
v14
```

## Hive API: stop, start and check the current state
* Check the current status of Hive Service (before stopping it): 
```
[root@amsterdam cloudera-scm-server]# curl -u AleNegrini:cloudera 'http://localhost:7180/api/v14/clusters/AleNegrini/services/hive/'
{
  "name" : "hive",
  "type" : "HIVE",
  "clusterRef" : {
    "clusterName" : "cluster"
  },
  "serviceUrl" : "http://amsterdam.c.sebc-labs.internal:7180/cmf/serviceRedirect/hive",
  "roleInstancesUrl" : "http://amsterdam.c.sebc-labs.internal:7180/cmf/serviceRedirect/hive/instances",
  "serviceState" : "STARTED",
  "healthSummary" : "GOOD",
  "healthChecks" : [ {
    "name" : "HIVE_HIVEMETASTORES_HEALTHY",
    "summary" : "GOOD",
    "suppressed" : false
  }, {
    "name" : "HIVE_HIVESERVER2S_HEALTHY",
    "summary" : "GOOD",
    "suppressed" : false
  } ],
  "configStalenessStatus" : "FRESH",
  "clientConfigStalenessStatus" : "FRESH",
  "maintenanceMode" : false,
  "maintenanceOwners" : [ ],
  "displayName" : "Hive",
  "entityStatus" : "GOOD_HEALTH"
}
```

* Stop Hive Service:
```
[root@amsterdam cloudera-scm-server]# curl -X POST -u AleNegrini:cloudera -w "\n" http://localhost:7180/api/v14/clusters/AleNegrini/services/hive/commands/stop
{
  "id" : 542,
  "name" : "Stop",
  "startTime" : "2018-03-14T09:43:39.148Z",
  "active" : true,
  "serviceRef" : {
    "clusterName" : "cluster",
    "serviceName" : "hive"
  }
}

```
* Check the new status of Hive Service (after stopping it): 
```
[root@amsterdam cloudera-scm-server]# curl -u AleNegrini:cloudera 'http://localhost:7180/api/v14/clusters/AleNegrini/services/hive/'           {
  "name" : "hive",
  "type" : "HIVE",
  "clusterRef" : {
    "clusterName" : "cluster"
  },
  "serviceUrl" : "http://amsterdam.c.sebc-labs.internal:7180/cmf/serviceRedirect/hive",
  "roleInstancesUrl" : "http://amsterdam.c.sebc-labs.internal:7180/cmf/serviceRedirect/hive/instances",
  "serviceState" : "STOPPED",
  "healthSummary" : "DISABLED",
  "healthChecks" : [ {
    "name" : "HIVE_HIVEMETASTORES_HEALTHY",
    "summary" : "DISABLED",
    "suppressed" : false
  }, {
    "name" : "HIVE_HIVESERVER2S_HEALTHY",
    "summary" : "DISABLED",
    "suppressed" : false
  } ],
  "configStalenessStatus" : "FRESH",
  "clientConfigStalenessStatus" : "FRESH",
  "maintenanceMode" : false,
  "maintenanceOwners" : [ ],
  "displayName" : "Hive",
  "entityStatus" : "STOPPED"
}
```
* Start Hive Service:
```
[root@amsterdam cloudera-scm-server]# curl X POST -u AleNegrini:cloudera -w "\n" http://localhost:7180/api/v2/clusters/AleNegrini/services/hive/commands/start
{
  "id" : 546,
  "name" : "Start",
  "startTime" : "2018-03-14T09:44:46.236Z",
  "active" : true,
  "serviceRef" : {
    "clusterName" : "cluster",
    "serviceName" : "hive"
  }
}
```
* Check the new status of Hive Service (after stopping it): 
```
[root@amsterdam cloudera-scm-server]# curl -u AleNegrini:cloudera 'http://localhost:7180/api/v14/clusters/AleNegrini/services/hive/'
{
  "name" : "hive",
  "type" : "HIVE",
  "clusterRef" : {
    "clusterName" : "cluster"
  },
  "serviceUrl" : "http://amsterdam.c.sebc-labs.internal:7180/cmf/serviceRedirect/hive",
  "roleInstancesUrl" : "http://amsterdam.c.sebc-labs.internal:7180/cmf/serviceRedirect/hive/instances",
  "serviceState" : "STARTED",
  "healthSummary" : "GOOD",
  "healthChecks" : [ {
    "name" : "HIVE_HIVEMETASTORES_HEALTHY",
    "summary" : "GOOD",
    "suppressed" : false
  }, {
    "name" : "HIVE_HIVESERVER2S_HEALTHY",
    "summary" : "GOOD",
    "suppressed" : false
  } ],
  "configStalenessStatus" : "FRESH",
  "clientConfigStalenessStatus" : "FRESH",
  "maintenanceMode" : false,
  "maintenanceOwners" : [ ],
  "displayName" : "Hive",
  "entityStatus" : "GOOD_HEALTH"
}
```
