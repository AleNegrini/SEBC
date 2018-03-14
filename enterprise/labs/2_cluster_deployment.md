# CM API 

## Output of API call using curl

Command launched on the CM host:
``` 
curl -u AleNegrini:cloudera -w "\n" http://localhost:7180/api/v2/cm/deployment
```

Result obtained: 
```
{
  "timestamp" : "2018-03-14T09:21:33.675Z",
  "clusters" : [ {
    "name" : "AleNegrini",
    "version" : "CDH5",
    "services" : [ {
      "name" : "hive",
      "type" : "HIVE",
      "config" : {
        "roleTypeConfigs" : [ {
          "roleType" : "HIVEMETASTORE",
          "items" : [ {
            "name" : "hive_metastore_java_heapsize",
            "value" : "782237696"
          } ]
        }, {
          "roleType" : "HIVESERVER2",
          "items" : [ {
            "name" : "hiveserver2_java_heapsize",
            "value" : "2001731584"
          }, {
            "name" : "hiveserver2_spark_driver_memory",
            "value" : "966367641"
          }, {
            "name" : "hiveserver2_spark_executor_cores",
            "value" : "2"
          }, {
            "name" : "hiveserver2_spark_executor_memory",
            "value" : "2805779660"
          }, {
            "name" : "hiveserver2_spark_yarn_driver_memory_overhead",
            "value" : "102"
          }, {
            "name" : "hiveserver2_spark_yarn_executor_memory_overhead",
            "value" : "472"
          } ]
        } ],
        "items" : [ {
          "name" : "hive_metastore_database_host",
          "value" : "amsterdam.c.sebc-labs.internal"
        }, {
          "name" : "hive_metastore_database_password",
          "value" : "hive_password"
        }, {
          "name" : "mapreduce_yarn_service",
          "value" : "yarn"
        }, {
          "name" : "zookeeper_service",
          "value" : "zookeeper"
        } ]
      },
      "roles" : [ {
        "name" : "hive-GATEWAY-2e8e526f2b458bb99fdb8c6970e60d9d",
        "type" : "GATEWAY",
        "hostRef" : {
          "hostId" : "7df1d8b4-ba65-4344-b111-0af2e7cc838d"
        },
        "config" : {
          "items" : [ ]
        }
      }, {
        "name" : "hive-GATEWAY-4a2bdbea8c760cbb8f0aea8402bf864d",
        "type" : "GATEWAY",
        "hostRef" : {
          "hostId" : "18659f34-066a-4952-af1f-9b208a223a43"
        },
        "config" : {
          "items" : [ ]
        }
      }, {
        "name" : "hive-GATEWAY-4cae428a0473a83646faef59ac196db6",
        "type" : "GATEWAY",
        "hostRef" : {
          "hostId" : "7afe583c-949a-483f-9dd8-0290aabe9dc4"
        },
        "config" : {
          "items" : [ ]
        }
      }, {
        "name" : "hive-GATEWAY-59b8e8182c02935e0f8a8ef46ee613fd",
        "type" : "GATEWAY",
        "hostRef" : {
          "hostId" : "ef956b05-6010-49cd-8df6-8d63f591049a"
        },
        "config" : {
          "items" : [ ]
        }
      }, {
        "name" : "hive-GATEWAY-d13cf07e51c6ba1367cb6597c9a8deb6",
        "type" : "GATEWAY",
        "hostRef" : {
          "hostId" : "bb977f38-2e72-4fc1-a9be-5b0933cb2820"
        },
        "config" : {
          "items" : [ ]
        }
      }, {
        "name" : "hive-HIVEMETASTORE-d13cf07e51c6ba1367cb6597c9a8deb6",
        "type" : "HIVEMETASTORE",
        "hostRef" : {
          "hostId" : "bb977f38-2e72-4fc1-a9be-5b0933cb2820"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "7bp9yogtcqlp285gzj7ka859b"
          } ]
        }
      }, {
        "name" : "hive-HIVESERVER2-2e8e526f2b458bb99fdb8c6970e60d9d",
        "type" : "HIVESERVER2",
        "hostRef" : {
          "hostId" : "7df1d8b4-ba65-4344-b111-0af2e7cc838d"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "3aouaphvroa8qt8l281csh5zf"
          } ]
        }
      } ],
      "displayName" : "Hive"
    }, {
      "name" : "zookeeper",
      "type" : "ZOOKEEPER",
      "config" : {
        "roleTypeConfigs" : [ {
          "roleType" : "SERVER",
          "items" : [ {
            "name" : "zookeeper_server_java_heapsize",
            "value" : "782237696"
          } ]
        } ],
        "items" : [ ]
      },
      "roles" : [ {
        "name" : "zookeeper-SERVER-2e8e526f2b458bb99fdb8c6970e60d9d",
        "type" : "SERVER",
        "hostRef" : {
          "hostId" : "7df1d8b4-ba65-4344-b111-0af2e7cc838d"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "elnlgeyzo7dtcnlpjageswkv2"
          }, {
            "name" : "serverId",
            "value" : "3"
          } ]
        }
      }, {
        "name" : "zookeeper-SERVER-4a2bdbea8c760cbb8f0aea8402bf864d",
        "type" : "SERVER",
        "hostRef" : {
          "hostId" : "18659f34-066a-4952-af1f-9b208a223a43"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "etj4c70f05bltivq9snu6m3v0"
          }, {
            "name" : "serverId",
            "value" : "2"
          } ]
        }
      }, {
        "name" : "zookeeper-SERVER-d13cf07e51c6ba1367cb6597c9a8deb6",
        "type" : "SERVER",
        "hostRef" : {
          "hostId" : "bb977f38-2e72-4fc1-a9be-5b0933cb2820"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "ce3dlu0a0licvnvwfuzognawq"
          }, {
            "name" : "serverId",
            "value" : "1"
          } ]
        }
      } ],
      "displayName" : "ZooKeeper"
    }, {
      "name" : "hue",
      "type" : "HUE",
      "config" : {
        "roleTypeConfigs" : [ ],
        "items" : [ {
          "name" : "database_host",
          "value" : "amsterdam.c.sebc-labs.internal"
        }, {
          "name" : "database_password",
          "value" : "hue_password"
        }, {
          "name" : "database_type",
          "value" : "mysql"
        }, {
          "name" : "hive_service",
          "value" : "hive"
        }, {
          "name" : "hue_webhdfs",
          "value" : "hdfs-HTTPFS-4cae428a0473a83646faef59ac196db6"
        }, {
          "name" : "oozie_service",
          "value" : "oozie"
        }, {
          "name" : "zookeeper_service",
          "value" : "zookeeper"
        } ]
      },
      "roles" : [ {
        "name" : "hue-HUE_SERVER-d13cf07e51c6ba1367cb6597c9a8deb6",
        "type" : "HUE_SERVER",
        "hostRef" : {
          "hostId" : "bb977f38-2e72-4fc1-a9be-5b0933cb2820"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "br1v42av682osihq2cb2ycdn7"
          }, {
            "name" : "secret_key",
            "value" : "BtM8C5vkXg0H5qAeFgY1o5ZvbrFfkv"
          } ]
        }
      } ],
      "displayName" : "Hue"
    }, {
      "name" : "oozie",
      "type" : "OOZIE",
      "config" : {
        "roleTypeConfigs" : [ {
          "roleType" : "OOZIE_SERVER",
          "items" : [ {
            "name" : "oozie_database_host",
            "value" : "amsterdam.c.sebc-labs.internal"
          }, {
            "name" : "oozie_database_password",
            "value" : "oozie_password"
          }, {
            "name" : "oozie_database_type",
            "value" : "mysql"
          }, {
            "name" : "oozie_database_user",
            "value" : "oozie"
          } ]
        } ],
        "items" : [ {
          "name" : "hive_service",
          "value" : "hive"
        }, {
          "name" : "mapreduce_yarn_service",
          "value" : "yarn"
        }, {
          "name" : "zookeeper_service",
          "value" : "zookeeper"
        } ]
      },
      "roles" : [ {
        "name" : "oozie-OOZIE_SERVER-2e8e526f2b458bb99fdb8c6970e60d9d",
        "type" : "OOZIE_SERVER",
        "hostRef" : {
          "hostId" : "7df1d8b4-ba65-4344-b111-0af2e7cc838d"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "8zps9i5jdqb1lx58t6yxocqlr"
          } ]
        }
      } ],
      "displayName" : "Oozie"
    }, {
      "name" : "yarn",
      "type" : "YARN",
      "config" : {
        "roleTypeConfigs" : [ {
          "roleType" : "GATEWAY",
          "items" : [ {
            "name" : "mapred_reduce_tasks",
            "value" : "3"
          }, {
            "name" : "mapred_submit_replication",
            "value" : "1"
          } ]
        }, {
          "roleType" : "NODEMANAGER",
          "items" : [ {
            "name" : "rm_cpu_shares",
            "value" : "1600"
          }, {
            "name" : "rm_io_weight",
            "value" : "800"
          }, {
            "name" : "yarn_nodemanager_heartbeat_interval_ms",
            "value" : "100"
          }, {
            "name" : "yarn_nodemanager_local_dirs",
            "value" : "/yarn/nm"
          }, {
            "name" : "yarn_nodemanager_log_dirs",
            "value" : "/yarn/container-logs"
          }, {
            "name" : "yarn_nodemanager_resource_cpu_vcores",
            "value" : "2"
          }, {
            "name" : "yarn_nodemanager_resource_memory_mb",
            "value" : "2866"
          } ]
        }, {
          "roleType" : "RESOURCEMANAGER",
          "items" : [ {
            "name" : "yarn_scheduler_maximum_allocation_mb",
            "value" : "2866"
          }, {
            "name" : "yarn_scheduler_maximum_allocation_vcores",
            "value" : "1"
          } ]
        } ],
        "items" : [ {
          "name" : "hdfs_service",
          "value" : "hdfs"
        }, {
          "name" : "rm_dirty",
          "value" : "true"
        }, {
          "name" : "rm_last_allocation_percentage",
          "value" : "80"
        }, {
          "name" : "yarn_service_cgroups",
          "value" : "false"
        }, {
          "name" : "yarn_service_lce_always",
          "value" : "false"
        }, {
          "name" : "zk_authorization_secret_key",
          "value" : "xJiD5h2PMRLkiXuXo0uWRw6QhNZFUo"
        }, {
          "name" : "zookeeper_service",
          "value" : "zookeeper"
        } ]
      },
      "roles" : [ {
        "name" : "yarn-JOBHISTORY-2e8e526f2b458bb99fdb8c6970e60d9d",
        "type" : "JOBHISTORY",
        "hostRef" : {
          "hostId" : "7df1d8b4-ba65-4344-b111-0af2e7cc838d"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "944n9td1w689ozwbb8ibtcy0v"
          } ]
        }
      }, {
        "name" : "yarn-NODEMANAGER-4a2bdbea8c760cbb8f0aea8402bf864d",
        "type" : "NODEMANAGER",
        "hostRef" : {
          "hostId" : "18659f34-066a-4952-af1f-9b208a223a43"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "c8v5xiswq2d40lkr99u3htg3u"
          } ]
        }
      }, {
        "name" : "yarn-NODEMANAGER-4cae428a0473a83646faef59ac196db6",
        "type" : "NODEMANAGER",
        "hostRef" : {
          "hostId" : "7afe583c-949a-483f-9dd8-0290aabe9dc4"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "82zbpaslovuerblepzrget05a"
          } ]
        }
      }, {
        "name" : "yarn-NODEMANAGER-59b8e8182c02935e0f8a8ef46ee613fd",
        "type" : "NODEMANAGER",
        "hostRef" : {
          "hostId" : "ef956b05-6010-49cd-8df6-8d63f591049a"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "1jzd42gqw3380b6ytus5n9a0p"
          } ]
        }
      }, {
        "name" : "yarn-RESOURCEMANAGER-2e8e526f2b458bb99fdb8c6970e60d9d",
        "type" : "RESOURCEMANAGER",
        "hostRef" : {
          "hostId" : "7df1d8b4-ba65-4344-b111-0af2e7cc838d"
        },
        "config" : {
          "items" : [ {
            "name" : "rm_id",
            "value" : "50"
          }, {
            "name" : "role_jceks_password",
            "value" : "1tupyxktf24qq2ywlw05yfdqm"
          } ]
        }
      } ],
      "displayName" : "YARN (MR2 Included)"
    }, {
      "name" : "hdfs",
      "type" : "HDFS",
      "config" : {
        "roleTypeConfigs" : [ {
          "roleType" : "BALANCER",
          "items" : [ {
            "name" : "balancer_java_heapsize",
            "value" : "782237696"
          } ]
        }, {
          "roleType" : "DATANODE",
          "items" : [ {
            "name" : "datanode_java_heapsize",
            "value" : "1073741824"
          }, {
            "name" : "dfs_data_dir_list",
            "value" : "/dfs/dn"
          }, {
            "name" : "dfs_datanode_du_reserved",
            "value" : "5367486464"
          }, {
            "name" : "dfs_datanode_max_locked_memory",
            "value" : "4294967296"
          }, {
            "name" : "rm_cpu_shares",
            "value" : "400"
          }, {
            "name" : "rm_io_weight",
            "value" : "200"
          } ]
        }, {
          "roleType" : "GATEWAY",
          "items" : [ {
            "name" : "dfs_client_use_trash",
            "value" : "true"
          } ]
        }, {
          "roleType" : "JOURNALNODE",
          "items" : [ {
            "name" : "dfs_journalnode_edits_dir",
            "value" : "/dfs/jn"
          } ]
        }, {
          "roleType" : "NAMENODE",
          "items" : [ {
            "name" : "dfs_name_dir_list",
            "value" : "/dfs/nn"
          }, {
            "name" : "dfs_namenode_servicerpc_address",
            "value" : "8022"
          }, {
            "name" : "namenode_java_heapsize",
            "value" : "782237696"
          } ]
        }, {
          "roleType" : "SECONDARYNAMENODE",
          "items" : [ {
            "name" : "fs_checkpoint_dir_list",
            "value" : "/dfs/snn"
          }, {
            "name" : "secondary_namenode_java_heapsize",
            "value" : "782237696"
          } ]
        } ],
        "items" : [ {
          "name" : "dfs_ha_fencing_cloudera_manager_secret_key",
          "value" : "FLkvliMZEwrRTKVuif6A9VZuNfAgUU"
        }, {
          "name" : "dfs_ha_fencing_methods",
          "value" : "shell(true)"
        }, {
          "name" : "fc_authorization_secret_key",
          "value" : "Ls9HTE5JPuOwVwl8k93iUdUA4bXiDM"
        }, {
          "name" : "http_auth_signature_secret",
          "value" : "bmtKiYo8zL2J31NxCOMza8hmjeWFYr"
        }, {
          "name" : "rm_dirty",
          "value" : "false"
        }, {
          "name" : "rm_last_allocation_percentage",
          "value" : "20"
        }, {
          "name" : "zookeeper_service",
          "value" : "zookeeper"
        } ]
      },
      "roles" : [ {
        "name" : "hdfs-BALANCER-d13cf07e51c6ba1367cb6597c9a8deb6",
        "type" : "BALANCER",
        "hostRef" : {
          "hostId" : "bb977f38-2e72-4fc1-a9be-5b0933cb2820"
        },
        "config" : {
          "items" : [ ]
        }
      }, {
        "name" : "hdfs-DATANODE-4a2bdbea8c760cbb8f0aea8402bf864d",
        "type" : "DATANODE",
        "hostRef" : {
          "hostId" : "18659f34-066a-4952-af1f-9b208a223a43"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "3gsy15gy5x1u169b3iiq7oc5y"
          } ]
        }
      }, {
        "name" : "hdfs-DATANODE-4cae428a0473a83646faef59ac196db6",
        "type" : "DATANODE",
        "hostRef" : {
          "hostId" : "7afe583c-949a-483f-9dd8-0290aabe9dc4"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "pqk5mskhv2wdjly93o5hu4qp"
          } ]
        }
      }, {
        "name" : "hdfs-DATANODE-59b8e8182c02935e0f8a8ef46ee613fd",
        "type" : "DATANODE",
        "hostRef" : {
          "hostId" : "ef956b05-6010-49cd-8df6-8d63f591049a"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "elbr9q8i0badb6bcowuzshng4"
          } ]
        }
      }, {
        "name" : "hdfs-FAILOVERCONTROLLER-2e8e526f2b458bb99fdb8c6970e60d9d",
        "type" : "FAILOVERCONTROLLER",
        "hostRef" : {
          "hostId" : "7df1d8b4-ba65-4344-b111-0af2e7cc838d"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "1r3yar4yb4njodhggsajopgb0"
          } ]
        }
      }, {
        "name" : "hdfs-FAILOVERCONTROLLER-d13cf07e51c6ba1367cb6597c9a8deb6",
        "type" : "FAILOVERCONTROLLER",
        "hostRef" : {
          "hostId" : "bb977f38-2e72-4fc1-a9be-5b0933cb2820"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "9pcdssf48b5xk1ozjrk5luyp3"
          } ]
        }
      }, {
        "name" : "hdfs-HTTPFS-4cae428a0473a83646faef59ac196db6",
        "type" : "HTTPFS",
        "hostRef" : {
          "hostId" : "7afe583c-949a-483f-9dd8-0290aabe9dc4"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "e0nl6yj2abuvaum80hu4f75bh"
          } ]
        }
      }, {
        "name" : "hdfs-JOURNALNODE-4a2bdbea8c760cbb8f0aea8402bf864d",
        "type" : "JOURNALNODE",
        "hostRef" : {
          "hostId" : "18659f34-066a-4952-af1f-9b208a223a43"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "cxq2dq59n31spam5u5ncjcxv7"
          } ]
        }
      }, {
        "name" : "hdfs-JOURNALNODE-4cae428a0473a83646faef59ac196db6",
        "type" : "JOURNALNODE",
        "hostRef" : {
          "hostId" : "7afe583c-949a-483f-9dd8-0290aabe9dc4"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "9wilp9my7o901776bestyyfyv"
          } ]
        }
      }, {
        "name" : "hdfs-JOURNALNODE-59b8e8182c02935e0f8a8ef46ee613fd",
        "type" : "JOURNALNODE",
        "hostRef" : {
          "hostId" : "ef956b05-6010-49cd-8df6-8d63f591049a"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "702fugx8eiqwx0l34ysbxol6i"
          } ]
        }
      }, {
        "name" : "hdfs-NAMENODE-2e8e526f2b458bb99fdb8c6970e60d9d",
        "type" : "NAMENODE",
        "hostRef" : {
          "hostId" : "7df1d8b4-ba65-4344-b111-0af2e7cc838d"
        },
        "config" : {
          "items" : [ {
            "name" : "autofailover_enabled",
            "value" : "true"
          }, {
            "name" : "dfs_federation_namenode_nameservice",
            "value" : "nameservice1"
          }, {
            "name" : "dfs_namenode_quorum_journal_name",
            "value" : "nameservice1"
          }, {
            "name" : "namenode_id",
            "value" : "57"
          }, {
            "name" : "role_jceks_password",
            "value" : "dycfdltdtdp46y3yal31f7hdy"
          } ]
        }
      }, {
        "name" : "hdfs-NAMENODE-d13cf07e51c6ba1367cb6597c9a8deb6",
        "type" : "NAMENODE",
        "hostRef" : {
          "hostId" : "bb977f38-2e72-4fc1-a9be-5b0933cb2820"
        },
        "config" : {
          "items" : [ {
            "name" : "autofailover_enabled",
            "value" : "true"
          }, {
            "name" : "dfs_federation_namenode_nameservice",
            "value" : "nameservice1"
          }, {
            "name" : "dfs_namenode_quorum_journal_name",
            "value" : "nameservice1"
          }, {
            "name" : "namenode_id",
            "value" : "52"
          }, {
            "name" : "role_jceks_password",
            "value" : "ev7gwdvg15wknpyjthorpvn52"
          } ]
        }
      } ],
      "displayName" : "HDFS"
    } ]
  } ],
  "hosts" : [ {
    "hostId" : "bb977f38-2e72-4fc1-a9be-5b0933cb2820",
    "ipAddress" : "10.142.0.2",
    "hostname" : "amsterdam.c.sebc-labs.internal",
    "rackId" : "/default",
    "config" : {
      "items" : [ ]
    }
  }, {
    "hostId" : "7df1d8b4-ba65-4344-b111-0af2e7cc838d",
    "ipAddress" : "10.142.0.3",
    "hostname" : "berlin.c.sebc-labs.internal",
    "rackId" : "/default",
    "config" : {
      "items" : [ ]
    }
  }, {
    "hostId" : "18659f34-066a-4952-af1f-9b208a223a43",
    "ipAddress" : "10.142.0.5",
    "hostname" : "london.c.sebc-labs.internal",
    "rackId" : "/default",
    "config" : {
      "items" : [ ]
    }
  }, {
    "hostId" : "7afe583c-949a-483f-9dd8-0290aabe9dc4",
    "ipAddress" : "10.142.0.6",
    "hostname" : "milan.c.sebc-labs.internal",
    "rackId" : "/default",
    "config" : {
      "items" : [ ]
    }
  }, {
    "hostId" : "ef956b05-6010-49cd-8df6-8d63f591049a",
    "ipAddress" : "10.142.0.4",
    "hostname" : "paris.c.sebc-labs.internal",
    "rackId" : "/default",
    "config" : {
      "items" : [ ]
    }
  } ],
  "users" : [ {
    "name" : "AleNegrini",
    "roles" : [ "ROLE_ADMIN" ],
    "pwHash" : "ece7e4a80346f2174e76c4d2fc157b517738337916e918bcd49375618626da2c",
    "pwSalt" : 1818481964926739567,
    "pwLogin" : true
  }, {
    "name" : "__cloudera_internal_user__mgmt-EVENTSERVER-d13cf07e51c6ba1367cb6597c9a8deb6",
    "roles" : [ "ROLE_USER" ],
    "pwHash" : "6cccc62260d377ca63d8aab5476da0219d9cfcf52370902317f63330252de0da",
    "pwSalt" : -3887334261107867691,
    "pwLogin" : true
  }, {
    "name" : "__cloudera_internal_user__mgmt-HOSTMONITOR-d13cf07e51c6ba1367cb6597c9a8deb6",
    "roles" : [ "ROLE_USER" ],
    "pwHash" : "7dfbba6404a69748646f64ebed46fb3f8afdc0e5c0e0ccc7e0959e5264f1b805",
    "pwSalt" : 7467389723855804083,
    "pwLogin" : true
  }, {
    "name" : "__cloudera_internal_user__mgmt-REPORTSMANAGER-d13cf07e51c6ba1367cb6597c9a8deb6",
    "roles" : [ "ROLE_USER" ],
    "pwHash" : "2df3098253db94202fb9aeb6b6c6aab538bc64d10b8f4f4f43b6d1b858678a8c",
    "pwSalt" : 7884483406497834605,
    "pwLogin" : true
  }, {
    "name" : "__cloudera_internal_user__mgmt-SERVICEMONITOR-d13cf07e51c6ba1367cb6597c9a8deb6",
    "roles" : [ "ROLE_USER" ],
    "pwHash" : "f18ac8c02c100844288c4548a787f08e25d9ac3815f4bd7560ceca5d204f8082",
    "pwSalt" : 6200839884869761233,
    "pwLogin" : true
  }, {
    "name" : "admin",
    "roles" : [ "ROLE_LIMITED" ],
    "pwHash" : "e6ec70c63863b8f8191e4ff41f6cc04b10bb9071af1310cf1416cf79e4c7f10a",
    "pwSalt" : -989304983258996394,
    "pwLogin" : true
  }, {
    "name" : "minotaur",
    "roles" : [ "ROLE_CONFIGURATOR" ],
    "pwHash" : "cd8807021deed67f80ed54be873fb2e493d10a7e74d35948904a8b6c284239e3",
    "pwSalt" : 1075792548787098782,
    "pwLogin" : true
  } ],
  "versionInfo" : {
    "version" : "5.9.3",
    "buildUser" : "jenkins",
    "buildTimestamp" : "20170627-1506",
    "gitHash" : "23506bb4e114dd460bdac64c57a672e6be631907",
    "snapshot" : false
  },
  "managementService" : {
    "name" : "mgmt",
    "type" : "MGMT",
    "config" : {
      "roleTypeConfigs" : [ {
        "roleType" : "EVENTSERVER",
        "items" : [ {
          "name" : "event_server_heapsize",
          "value" : "782237696"
        } ]
      }, {
        "roleType" : "HOSTMONITOR",
        "items" : [ {
          "name" : "firehose_heapsize",
          "value" : "782237696"
        }, {
          "name" : "firehose_non_java_memory_bytes",
          "value" : "1017118720"
        } ]
      }, {
        "roleType" : "REPORTSMANAGER",
        "items" : [ {
          "name" : "headlamp_database_host",
          "value" : "amsterdam.c.sebc-labs.internal"
        }, {
          "name" : "headlamp_database_name",
          "value" : "rman"
        }, {
          "name" : "headlamp_database_password",
          "value" : "rman_password"
        }, {
          "name" : "headlamp_database_user",
          "value" : "rman"
        }, {
          "name" : "headlamp_heapsize",
          "value" : "782237696"
        } ]
      }, {
        "roleType" : "SERVICEMONITOR",
        "items" : [ {
          "name" : "firehose_heapsize",
          "value" : "782237696"
        }, {
          "name" : "firehose_non_java_memory_bytes",
          "value" : "1017118720"
        } ]
      } ],
      "items" : [ ]
    },
    "roles" : [ {
      "name" : "mgmt-ALERTPUBLISHER-d13cf07e51c6ba1367cb6597c9a8deb6",
      "type" : "ALERTPUBLISHER",
      "hostRef" : {
        "hostId" : "bb977f38-2e72-4fc1-a9be-5b0933cb2820"
      },
      "config" : {
        "items" : [ {
          "name" : "role_jceks_password",
          "value" : "ebdhz6exqm4j2m1ylobzyewk"
        } ]
      }
    }, {
      "name" : "mgmt-EVENTSERVER-d13cf07e51c6ba1367cb6597c9a8deb6",
      "type" : "EVENTSERVER",
      "hostRef" : {
        "hostId" : "bb977f38-2e72-4fc1-a9be-5b0933cb2820"
      },
      "config" : {
        "items" : [ {
          "name" : "role_jceks_password",
          "value" : "9g8j59wdhtsb97zib6c8gpyo3"
        } ]
      }
    }, {
      "name" : "mgmt-HOSTMONITOR-d13cf07e51c6ba1367cb6597c9a8deb6",
      "type" : "HOSTMONITOR",
      "hostRef" : {
        "hostId" : "bb977f38-2e72-4fc1-a9be-5b0933cb2820"
      },
      "config" : {
        "items" : [ {
          "name" : "role_jceks_password",
          "value" : "5c13r1zj2n2h8dtq39eeo1nwu"
        } ]
      }
    }, {
      "name" : "mgmt-REPORTSMANAGER-d13cf07e51c6ba1367cb6597c9a8deb6",
      "type" : "REPORTSMANAGER",
      "hostRef" : {
        "hostId" : "bb977f38-2e72-4fc1-a9be-5b0933cb2820"
      },
      "config" : {
        "items" : [ {
          "name" : "role_jceks_password",
          "value" : "6vebjpps6jc920z3g6v4bg6t"
        } ]
      }
    }, {
      "name" : "mgmt-SERVICEMONITOR-d13cf07e51c6ba1367cb6597c9a8deb6",
      "type" : "SERVICEMONITOR",
      "hostRef" : {
        "hostId" : "bb977f38-2e72-4fc1-a9be-5b0933cb2820"
      },
      "config" : {
        "items" : [ {
          "name" : "role_jceks_password",
          "value" : "6wg0dcx13htuhala0ma6ufkb"
        } ]
      }
    } ],
    "displayName" : "Cloudera Management Service"
  },
  "managerSettings" : {
    "items" : [ {
      "name" : "CLUSTER_STATS_START",
      "value" : "10/23/2012 15:10"
    }, {
      "name" : "PUBLIC_CLOUD_STATUS",
      "value" : "NOT_ON_PUBLIC_CLOUD"
    }, {
      "name" : "REMOTE_PARCEL_REPO_URLS",
      "value" : "https://archive.cloudera.com/cdh5/parcels/{latest_supported}/,https://archive.cloudera.com/cdh4/parcels/latest/,https://archive.cloudera.com/impala/parcels/latest/,https://archive.cloudera.com/search/parcels/latest/,https://archive.cloudera.com/accumulo/parcels/1.4/,https://archive.cloudera.com/accumulo-c5/parcels/latest/,https://archive.cloudera.com/kafka/parcels/latest/,https://archive.cloudera.com/navigator-keytrustee5/parcels/latest/,https://archive.cloudera.com/spark/parcels/latest/,https://archive.cloudera.com/sqoop-connectors/parcels/latest/,http://localhost/cdh/"
    } ]
  }
}
```
