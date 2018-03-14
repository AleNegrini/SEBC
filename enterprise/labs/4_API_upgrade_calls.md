# CM Upgrade


## Before the upgrade
* Report the latest available version of the API
```
[root@amsterdam cloudera-scm-server]# curl u AleNegrini:cloudera 'http://localhost:7180/api/version'                                          
v14
```

* Report the CM version
```
[root@amsterdam cloudera-scm-server]# curl -u AleNegrini:cloudera 'http://localhost:7180/api/v14/cm/version'
{
  "version" : "5.9.3",
  "buildUser" : "jenkins",
  "buildTimestamp" : "20170627-1506",
  "gitHash" : "23506bb4e114dd460bdac64c57a672e6be631907",
  "snapshot" : false
}
```

* List all CM users
```
[root@amsterdam cloudera-scm-server]# curl -u AleNegrini:cloudera 'http://localhost:7180/api/v14/users'
{
  "items" : [ {
    "name" : "AleNegrini",
    "roles" : [ "ROLE_ADMIN" ]
  }, {
    "name" : "admin",
    "roles" : [ "ROLE_LIMITED" ]
  }, {
    "name" : "minotaur",
    "roles" : [ "ROLE_CONFIGURATOR" ]
  } ]
}
```

* Report the database server type in use by CM (mysql, oracle, ...)
```
[root@amsterdam cloudera-scm-server]# curl -u AleNegrini:cloudera 'http://localhost:7180/api/v14/cm/scmDbInfo'
{
  "scmDbType" : "MYSQL",
  "embeddedDbUsed" : false
}
```

## After the upgrade
* Report the latest available version of the API
```
[root@amsterdam cloudera-scm-server]# curl u AleNegrini:cloudera 'http://localhost:7180/api/version'                                          
v19
```

* Report the CM version
```
[root@amsterdam yum.repos.d]# curl -u AleNegrini:cloudera 'http://localhost:7180/api/v14/cm/version'
{
  "version" : "5.14.1",
  "buildUser" : "jenkins",
  "buildTimestamp" : "20180207-1728",
  "gitHash" : "f253d8e2b9cf5cb61a2f1ba1bf71de6fb603add0",
  "snapshot" : false
}
```

* List all CM users
```
[root@amsterdam yum.repos.d]# curl -u AleNegrini:cloudera 'http://localhost:7180/api/v14/users'
{
  "items" : [ {
    "name" : "AleNegrini",
    "roles" : [ "ROLE_ADMIN" ]
  }, {
    "name" : "admin",
    "roles" : [ "ROLE_LIMITED" ]
  }, {
    "name" : "minotaur",
    "roles" : [ "ROLE_CONFIGURATOR" ]
  } ]
}
```

* Report the database server type in use by CM (mysql, oracle, ...)
```
[root@amsterdam cloudera-scm-server]# curl -u AleNegrini:cloudera 'http://localhost:718/api/v14/cm/scmDbInfo'
{
  "scmDbType" : "MYSQL",
  "embeddedDbUsed" : false
}
```