# MariaDB installation

The following instruction were run on the amsterdam host if not specifed differently, as my first node listed in `0_setup.md` file. 

Getting first node fully qualified domain name: 
```
[root@amsterdam tmp]# hostname --fqdn
amsterdam.c.sebc-pre-challenges.internal
```

Creating a MariaDB file repo with the following content: 
```
[mariadb]
name = MariaDB
baseurl = http://yum.mariadb.org/10.1/centos7-amd64
gpgkey=https://yum.mariadb.org/RPM-GPG-KEY-MariaDB
gpgcheck=1
```

Checking the repo: 
```
[root@amsterdam yum.repos.d]# sudo yum repolist enabled | grep "mariadb"
mariadb                 MariaDB                                               17
```

Installing MariaDB server on amsterdam host:
```
[root@amsterdam yum.repos.d]# sudo yum install MariaDB-server
Loaded plugins: fastestmirror
Loading mirror speeds from cached hostfile
 * base: mirror.wdc1.us.leaseweb.net
 * epel: mirror.us.leaseweb.net
 * extras: mirror.rackspace.com
 * updates: mirrors.centos.webair.com
Resolving Dependencies
--> Running transaction check
---> Package MariaDB-server.x86_64 0:10.1.31-1.el7.centos will be installed
--> Processing Dependency: MariaDB-client for package: MariaDB-server-10.1.31-1.el7.centos.x86_64
--> Processing Dependency: perl(DBI) for package: MariaDB-server-10.1.31-1.el7.centos.x86_64
--> Processing Dependency: galera for package: MariaDB-server-10.1.31-1.el7.centos.x86_64
--> Processing Dependency: MariaDB-common for package: MariaDB-server-10.1.31-1.el7.centos.x86_64
--> Processing Dependency: libaio.so.1(LIBAIO_0.1)(64bit) for package: MariaDB-server-10.1.31-1.el7.centos.x86_64
--> Processing Dependency: lsof for package: MariaDB-server-10.1.31-1.el7.centos.x86_64
--> Processing Dependency: libaio.so.1(LIBAIO_0.4)(64bit) for package: MariaDB-server-10.1.31-1.el7.centos.x86_64
--> Processing Dependency: perl(Data::Dumper) for package: MariaDB-server-10.1.31-1.el7.centos.x86_64
--> Processing Dependency: libaio.so.1()(64bit) for package: MariaDB-server-10.1.31-1.el7.centos.x86_64
--> Processing Dependency: libjemalloc.so.1()(64bit) for package: MariaDB-server-10.1.31-1.el7.centos.x86_64
--> Running transaction check
---> Package MariaDB-client.x86_64 0:10.1.31-1.el7.centos will be installed
---> Package MariaDB-common.x86_64 0:10.1.31-1.el7.centos will be installed
---> Package galera.x86_64 0:25.3.22-1.rhel7.el7.centos will be installed
--> Processing Dependency: libboost_program_options.so.1.53.0()(64bit) for package: galera-25.3.22-1.rhel7.el7.centos.x86_64
---> Package jemalloc.x86_64 0:3.6.0-1.el7 will be installed
---> Package libaio.x86_64 0:0.3.109-13.el7 will be installed
---> Package lsof.x86_64 0:4.87-4.el7 will be installed
---> Package perl-DBI.x86_64 0:1.627-4.el7 will be installed
--> Processing Dependency: perl(RPC::PlServer) >= 0.2001 for package: perl-DBI-1.627-4.el7.x86_64
--> Processing Dependency: perl(RPC::PlClient) >= 0.2000 for package: perl-DBI-1.627-4.el7.x86_64
---> Package perl-Data-Dumper.x86_64 0:2.145-3.el7 will be installed
--> Running transaction check
---> Package boost-program-options.x86_64 0:1.53.0-27.el7 will be installed
---> Package perl-PlRPC.noarch 0:0.2020-14.el7 will be installed
--> Processing Dependency: perl(Net::Daemon) >= 0.13 for package: perl-PlRPC-0.2020-14.el7.noarch
--> Processing Dependency: perl(Net::Daemon::Test) for package: perl-PlRPC-0.2020-14.el7.noarch
--> Processing Dependency: perl(Net::Daemon::Log) for package: perl-PlRPC-0.2020-14.el7.noarch
--> Processing Dependency: perl(Compress::Zlib) for package: perl-PlRPC-0.2020-14.el7.noarch
--> Running transaction check
---> Package perl-IO-Compress.noarch 0:2.061-2.el7 will be installed
--> Processing Dependency: perl(Compress::Raw::Zlib) >= 2.061 for package: perl-IO-Compress-2.061-2.el7.noarch
--> Processing Dependency: perl(Compress::Raw::Bzip2) >= 2.061 for package: perl-IO-Compress-2.061-2.el7.noarch
---> Package perl-Net-Daemon.noarch 0:0.48-5.el7 will be installed
--> Running transaction check
---> Package perl-Compress-Raw-Bzip2.x86_64 0:2.061-3.el7 will be installed
---> Package perl-Compress-Raw-Zlib.x86_64 1:2.061-4.el7 will be installed
--> Processing Conflict: MariaDB-common-10.1.31-1.el7.centos.x86_64 conflicts mariadb-libs < 1:10.1.31-1.el7.centos
--> Restarting Dependency Resolution with new changes.
--> Running transaction check
---> Package MariaDB-shared.x86_64 0:10.1.31-1.el7.centos will be obsoleting
---> Package mariadb-libs.x86_64 1:5.5.56-2.el7 will be obsoleted
--> Finished Dependency Resolution

Dependencies Resolved

================================================================================
 Package                  Arch    Version                        Repository
                                                                           Size
================================================================================
Installing:
 MariaDB-server           x86_64  10.1.31-1.el7.centos           mariadb  104 M
 MariaDB-shared           x86_64  10.1.31-1.el7.centos           mariadb  1.3 M
     replacing  mariadb-libs.x86_64 1:5.5.56-2.el7
Installing for dependencies:
 MariaDB-client           x86_64  10.1.31-1.el7.centos           mariadb   39 M
 MariaDB-common           x86_64  10.1.31-1.el7.centos           mariadb  123 k
 boost-program-options    x86_64  1.53.0-27.el7                  base     156 k
 galera                   x86_64  25.3.22-1.rhel7.el7.centos     mariadb  8.0 M
 jemalloc                 x86_64  3.6.0-1.el7                    epel     105 k
 libaio                   x86_64  0.3.109-13.el7                 base      24 k
 lsof                     x86_64  4.87-4.el7                     base     331 k
 perl-Compress-Raw-Bzip2  x86_64  2.061-3.el7                    base      32 k
 perl-Compress-Raw-Zlib   x86_64  1:2.061-4.el7                  base      57 k
 perl-DBI                 x86_64  1.627-4.el7                    base     802 k
 perl-Data-Dumper         x86_64  2.145-3.el7                    base      47 k
 perl-IO-Compress         noarch  2.061-2.el7                    base     260 k
 perl-Net-Daemon          noarch  0.48-5.el7                     base      51 k
 perl-PlRPC               noarch  0.2020-14.el7                  base      36 k

Transaction Summary
================================================================================
Install  2 Packages (+14 Dependent packages)

Total download size: 155 M
Is this ok [y/d/N]: y
Downloading packages:
warning: /var/cache/yum/x86_64/7/mariadb/packages/MariaDB-10.1.31-centos73-x86_64-common.rpm: Header V4 DSA/SHA1 Signature, key ID 1bb943db: NOKEY
Public key for MariaDB-10.1.31-centos73-x86_64-common.rpm is not installed
(1/16): MariaDB-10.1.31-centos73-x86_64-common.rpm         | 123 kB   00:00
(2/16): MariaDB-10.1.31-centos73-x86_64-client.rpm         |  39 MB   00:01
(3/16): MariaDB-10.1.31-centos73-x86_64-shared.rpm         | 1.3 MB   00:00
(4/16): libaio-0.3.109-13.el7.x86_64.rpm                   |  24 kB   00:00
(5/16): galera-25.3.22-1.rhel7.el7.centos.x86_64.rpm       | 8.0 MB   00:00
(6/16): jemalloc-3.6.0-1.el7.x86_64.rpm                    | 105 kB   00:00
(7/16): lsof-4.87-4.el7.x86_64.rpm                         | 331 kB   00:00
(8/16): perl-Compress-Raw-Bzip2-2.061-3.el7.x86_64.rpm     |  32 kB   00:00
(9/16): perl-Compress-Raw-Zlib-2.061-4.el7.x86_64.rpm      |  57 kB   00:00
(10/16): perl-Data-Dumper-2.145-3.el7.x86_64.rpm           |  47 kB   00:00
(11/16): perl-DBI-1.627-4.el7.x86_64.rpm                   | 802 kB   00:00
(12/16): perl-PlRPC-0.2020-14.el7.noarch.rpm               |  36 kB   00:00
(13/16): perl-Net-Daemon-0.48-5.el7.noarch.rpm             |  51 kB   00:00
(14/16): perl-IO-Compress-2.061-2.el7.noarch.rpm           | 260 kB   00:00
(15/16): MariaDB-10.1.31-centos73-x86_64-server.rpm        | 104 MB   00:02
(16/16): boost-program-options-1.53.0-27.el7.x86_64.rpm    | 156 kB   00:05
--------------------------------------------------------------------------------
Total                                               23 MB/s | 155 MB  00:06
Retrieving key from https://yum.mariadb.org/RPM-GPG-KEY-MariaDB
Importing GPG key 0x1BB943DB:
 Userid     : "MariaDB Package Signing Key <package-signing-key@mariadb.org>"
 Fingerprint: 1993 69e5 404b d5fc 7d2f e43b cbcb 082a 1bb9 43db
 From       : https://yum.mariadb.org/RPM-GPG-KEY-MariaDB
Is this ok [y/N]: y
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Installing : MariaDB-common-10.1.31-1.el7.centos.x86_64                  1/17
  Installing : libaio-0.3.109-13.el7.x86_64                                2/17
  Installing : perl-Data-Dumper-2.145-3.el7.x86_64                         3/17
  Installing : MariaDB-client-10.1.31-1.el7.centos.x86_64                  4/17
  Installing : boost-program-options-1.53.0-27.el7.x86_64                  5/17
  Installing : galera-25.3.22-1.rhel7.el7.centos.x86_64                    6/17
  Installing : perl-Compress-Raw-Bzip2-2.061-3.el7.x86_64                  7/17
  Installing : 1:perl-Compress-Raw-Zlib-2.061-4.el7.x86_64                 8/17
  Installing : perl-IO-Compress-2.061-2.el7.noarch                         9/17
  Installing : lsof-4.87-4.el7.x86_64                                     10/17
  Installing : jemalloc-3.6.0-1.el7.x86_64                                11/17
  Installing : perl-Net-Daemon-0.48-5.el7.noarch                          12/17
  Installing : perl-PlRPC-0.2020-14.el7.noarch                            13/17
  Installing : perl-DBI-1.627-4.el7.x86_64                                14/17
  Installing : MariaDB-server-10.1.31-1.el7.centos.x86_64                 15/17
chown: invalid user: ‘mysql’
2018-03-16  8:28:54 140639179884800 [Note] /usr/sbin/mysqld (mysqld 10.1.31-MariaDB) starting as process 2610 ...
2018-03-16  8:28:54 140639179884800 [Note] InnoDB: innodb_empty_free_list_algorithm has been changed to legacy because of small buffer pool size. In order to use backoff, increase buffer pool at least up to 20MB.

2018-03-16  8:28:54 140639179884800 [Note] InnoDB: Using mutexes to ref count buffer pool pages
2018-03-16  8:28:54 140639179884800 [Note] InnoDB: The InnoDB memory heap is disabled
2018-03-16  8:28:54 140639179884800 [Note] InnoDB: Mutexes and rw_locks use GCC atomic builtins
2018-03-16  8:28:54 140639179884800 [Note] InnoDB: GCC builtin __atomic_thread_fence() is used for memory barrier
2018-03-16  8:28:54 140639179884800 [Note] InnoDB: Compressed tables use zlib 1.2.7
2018-03-16  8:28:54 140639179884800 [Note] InnoDB: Using Linux native AIO
2018-03-16  8:28:54 140639179884800 [Note] InnoDB: Using SSE crc32 instructions
2018-03-16  8:28:54 140639179884800 [Note] InnoDB: Initializing buffer pool, size = 128.0M
2018-03-16  8:28:54 140639179884800 [Note] InnoDB: Completed initialization of buffer pool
2018-03-16  8:28:54 140639179884800 [Note] InnoDB: The first specified data file ./ibdata1 did not exist: a new database to be created!
2018-03-16  8:28:54 140639179884800 [Note] InnoDB: Setting file ./ibdata1 size to 12 MB
2018-03-16  8:28:54 140639179884800 [Note] InnoDB: Setting log file ./ib_logfile101 size to 48 MB
2018-03-16  8:28:55 140639179884800 [Note] InnoDB: Setting log file ./ib_logfile1 size to 48 MB
2018-03-16  8:28:55 140639179884800 [Note] InnoDB: Renaming log file ./ib_logfile101 to ./ib_logfile0
2018-03-16  8:28:55 140639179884800 [Warning] InnoDB: New log files created, LSN=45781
2018-03-16  8:28:55 140639179884800 [Note] InnoDB: Doublewrite buffer not found: creating new
2018-03-16  8:28:55 140639179884800 [Note] InnoDB: Doublewrite buffer created
2018-03-16  8:28:55 140639179884800 [Note] InnoDB: 128 rollback segment(s) are active.
2018-03-16  8:28:55 140639179884800 [Warning] InnoDB: Creating foreign key constraint system tables.
2018-03-16  8:28:55 140639179884800 [Note] InnoDB: Foreign key constraint system tables created
2018-03-16  8:28:55 140639179884800 [Note] InnoDB: Creating tablespace and datafile system tables.
2018-03-16  8:28:55 140639179884800 [Note] InnoDB: Tablespace and datafile system tables created.
2018-03-16  8:28:55 140639179884800 [Note] InnoDB: Waiting for purge to start
2018-03-16  8:28:55 140639179884800 [Note] InnoDB:  Percona XtraDB (http://www.percona.com) 5.6.36-83.0 started; log sequence number 0
2018-03-16  8:28:55 140638393726720 [Note] InnoDB: Dumping buffer pool(s) not yet started
2018-03-16  8:28:58 140014552279296 [Note] /usr/sbin/mysqld (mysqld 10.1.31-MariaDB) starting as process 2639 ...
2018-03-16  8:28:58 140014552279296 [Note] InnoDB: innodb_empty_free_list_algorithm has been changed to legacy because of small buffer pool size. In order to use backoff, increase buffer pool at least up to 20MB.

2018-03-16  8:28:58 140014552279296 [Note] InnoDB: Using mutexes to ref count buffer pool pages
2018-03-16  8:28:58 140014552279296 [Note] InnoDB: The InnoDB memory heap is disabled
2018-03-16  8:28:58 140014552279296 [Note] InnoDB: Mutexes and rw_locks use GCC atomic builtins
2018-03-16  8:28:58 140014552279296 [Note] InnoDB: GCC builtin __atomic_thread_fence() is used for memory barrier
2018-03-16  8:28:58 140014552279296 [Note] InnoDB: Compressed tables use zlib 1.2.7
2018-03-16  8:28:58 140014552279296 [Note] InnoDB: Using Linux native AIO
2018-03-16  8:28:58 140014552279296 [Note] InnoDB: Using SSE crc32 instructions
2018-03-16  8:28:58 140014552279296 [Note] InnoDB: Initializing buffer pool, size = 128.0M
2018-03-16  8:28:58 140014552279296 [Note] InnoDB: Completed initialization of buffer pool
2018-03-16  8:28:58 140014552279296 [Note] InnoDB: Highest supported file format is Barracuda.
2018-03-16  8:28:58 140014552279296 [Note] InnoDB: 128 rollback segment(s) are active.
2018-03-16  8:28:58 140014552279296 [Note] InnoDB: Waiting for purge to start
2018-03-16  8:28:58 140014552279296 [Note] InnoDB:  Percona XtraDB (http://www.percona.com) 5.6.36-83.0 started; log sequence number 1616697
2018-03-16  8:28:58 140013769586432 [Note] InnoDB: Dumping buffer pool(s) not yet started
2018-03-16  8:29:01 139700270004480 [Note] /usr/sbin/mysqld (mysqld 10.1.31-MariaDB) starting as process 2669 ...
2018-03-16  8:29:01 139700270004480 [Note] InnoDB: innodb_empty_free_list_algorithm has been changed to legacy because of small buffer pool size. In order to use backoff, increase buffer pool at least up to 20MB.

2018-03-16  8:29:01 139700270004480 [Note] InnoDB: Using mutexes to ref count buffer pool pages
2018-03-16  8:29:01 139700270004480 [Note] InnoDB: The InnoDB memory heap is disabled
2018-03-16  8:29:01 139700270004480 [Note] InnoDB: Mutexes and rw_locks use GCC atomic builtins
2018-03-16  8:29:01 139700270004480 [Note] InnoDB: GCC builtin __atomic_thread_fence() is used for memory barrier
2018-03-16  8:29:01 139700270004480 [Note] InnoDB: Compressed tables use zlib 1.2.7
2018-03-16  8:29:01 139700270004480 [Note] InnoDB: Using Linux native AIO
2018-03-16  8:29:01 139700270004480 [Note] InnoDB: Using SSE crc32 instructions
2018-03-16  8:29:01 139700270004480 [Note] InnoDB: Initializing buffer pool, size = 128.0M
2018-03-16  8:29:01 139700270004480 [Note] InnoDB: Completed initialization of buffer pool
2018-03-16  8:29:01 139700270004480 [Note] InnoDB: Highest supported file format is Barracuda.
2018-03-16  8:29:02 139700270004480 [Note] InnoDB: 128 rollback segment(s) are active.
2018-03-16  8:29:02 139700270004480 [Note] InnoDB: Waiting for purge to start
2018-03-16  8:29:02 139700270004480 [Note] InnoDB:  Percona XtraDB (http://www.percona.com) 5.6.36-83.0 started; log sequence number 1616707
2018-03-16  8:29:02 139699494577920 [Note] InnoDB: Dumping buffer pool(s) not yet started

PLEASE REMEMBER TO SET A PASSWORD FOR THE MariaDB root USER !
To do so, start the server, then issue the following commands:

'/usr/bin/mysqladmin' -u root password 'new-password'
'/usr/bin/mysqladmin' -u root -h amsterdam password 'new-password'

Alternatively you can run:
'/usr/bin/mysql_secure_installation'

which will also give you the option of removing the test
databases and anonymous user created by default.  This is
strongly recommended for production servers.

See the MariaDB Knowledgebase at http://mariadb.com/kb or the
MySQL manual for more instructions.

Please report any problems at http://mariadb.org/jira

The latest information about MariaDB is available at http://mariadb.org/.
You can find additional information about the MySQL part at:
http://dev.mysql.com
Consider joining MariaDB's strong and vibrant community:
https://mariadb.org/get-involved/

  Installing : MariaDB-shared-10.1.31-1.el7.centos.x86_64                 16/17
  Erasing    : 1:mariadb-libs-5.5.56-2.el7.x86_64                         17/17
  Verifying  : MariaDB-server-10.1.31-1.el7.centos.x86_64                  1/17
  Verifying  : perl-Net-Daemon-0.48-5.el7.noarch                           2/17
  Verifying  : perl-Data-Dumper-2.145-3.el7.x86_64                         3/17
  Verifying  : MariaDB-shared-10.1.31-1.el7.centos.x86_64                  4/17
  Verifying  : jemalloc-3.6.0-1.el7.x86_64                                 5/17
  Verifying  : lsof-4.87-4.el7.x86_64                                      6/17
  Verifying  : perl-IO-Compress-2.061-2.el7.noarch                         7/17
  Verifying  : MariaDB-common-10.1.31-1.el7.centos.x86_64                  8/17
  Verifying  : galera-25.3.22-1.rhel7.el7.centos.x86_64                    9/17
  Verifying  : 1:perl-Compress-Raw-Zlib-2.061-4.el7.x86_64                10/17
  Verifying  : MariaDB-client-10.1.31-1.el7.centos.x86_64                 11/17
  Verifying  : perl-Compress-Raw-Bzip2-2.061-3.el7.x86_64                 12/17
  Verifying  : boost-program-options-1.53.0-27.el7.x86_64                 13/17
  Verifying  : perl-DBI-1.627-4.el7.x86_64                                14/17
  Verifying  : libaio-0.3.109-13.el7.x86_64                               15/17
  Verifying  : perl-PlRPC-0.2020-14.el7.noarch                            16/17
  Verifying  : 1:mariadb-libs-5.5.56-2.el7.x86_64                         17/17

Installed:
  MariaDB-server.x86_64 0:10.1.31-1.el7.centos
  MariaDB-shared.x86_64 0:10.1.31-1.el7.centos

Dependency Installed:
  MariaDB-client.x86_64 0:10.1.31-1.el7.centos
  MariaDB-common.x86_64 0:10.1.31-1.el7.centos
  boost-program-options.x86_64 0:1.53.0-27.el7
  galera.x86_64 0:25.3.22-1.rhel7.el7.centos
  jemalloc.x86_64 0:3.6.0-1.el7
  libaio.x86_64 0:0.3.109-13.el7
  lsof.x86_64 0:4.87-4.el7
  perl-Compress-Raw-Bzip2.x86_64 0:2.061-3.el7
  perl-Compress-Raw-Zlib.x86_64 1:2.061-4.el7
  perl-DBI.x86_64 0:1.627-4.el7
  perl-Data-Dumper.x86_64 0:2.145-3.el7
  perl-IO-Compress.noarch 0:2.061-2.el7
  perl-Net-Daemon.noarch 0:0.48-5.el7
  perl-PlRPC.noarch 0:0.2020-14.el7

Replaced:
  mariadb-libs.x86_64 1:5.5.56-2.el7

Complete!

```

Checking the Mariadb version installed:
```
[root@amsterdam yum.repos.d]# mysql --version
mysql  Ver 15.1 Distrib 10.1.31-MariaDB, for Linux (x86_64) using readline 5.1
```

Before starting it, configure the `my.cnf` file as specified in the documentation: 
Before running it, we should configure the my.cnf file:
```
[mysqld]
transaction-isolation = READ-COMMITTED

key_buffer = 16M
key_buffer_size = 32M
max_allowed_packet = 32M
thread_stack = 256K
thread_cache_size = 64
query_cache_limit = 8M
query_cache_size = 64M
query_cache_type = 1

max_connections = 550

log_bin=/var/lib/mysql/mysql_binary_log

# For MySQL version 5.1.8 or later. Comment out binlog_format for older versions.
binlog_format = mixed

read_buffer_size = 2M
read_rnd_buffer_size = 16M
sort_buffer_size = 8M
join_buffer_size = 8M

# InnoDB settings
innodb_file_per_table = 1
innodb_flush_log_at_trx_commit  = 2
innodb_log_buffer_size = 64M
innodb_buffer_pool_size = 4G
innodb_thread_concurrency = 8
innodb_flush_method = O_DIRECT
innodb_log_file_size = 512M

[mysqld_safe]
log-error=/var/log/mysqld.log
pid-file=/var/run/mysqld/mysqld.pid

sql_mode=STRICT_ALL_TABLES
```

Installing the MariaDB client on all the hosts: 

Installing the JDBC driver on all the hosts. For that purpose I have written an ad hoc script that makes it: 
```
[root@amsterdam tmp]# ./jdbc.sh
--2018-03-15 13:02:58--  http://dev.mysql.com/get/Downloads/Connector-J/mysql-connector-java-5.1.40.tar.gz
Resolving dev.mysql.com (dev.mysql.com)... 137.254.60.11
Connecting to dev.mysql.com (dev.mysql.com)|137.254.60.11|:80... connected.
HTTP request sent, awaiting response... 301 Moved Permanently
Location: https://dev.mysql.com/get/Downloads/Connector-J/mysql-connector-java-5.1.40.tar.gz [following]
--2018-03-15 13:02:59--  https://dev.mysql.com/get/Downloads/Connector-J/mysql-connector-java-5.1.40.tar.gz
Connecting to dev.mysql.com (dev.mysql.com)|137.254.60.11|:443... connected.
HTTP request sent, awaiting response... 302 Found
Location: https://cdn.mysql.com//archives/mysql-connector-java-5.1/mysql-connector-java-5.1.40.tar.gz [following]
--2018-03-15 13:02:59--  https://cdn.mysql.com//archives/mysql-connector-java-5.1/mysql-connector-java-5.1.40.tar.gz
Resolving cdn.mysql.com (cdn.mysql.com)... 23.198.6.197
Connecting to cdn.mysql.com (cdn.mysql.com)|23.198.6.197|:443... connected.
HTTP request sent, awaiting response... 200 OK

```

Here below the body of the script: 
```
#!/bin/bash
cd /tmp/
wget http://dev.mysql.com/get/Downloads/Connector-J/mysql-connector-java-5.1.40.tar.gz
tar -zxvf mysql-connector-java-5.1.40.tar.gz
sudo mkdir -p /usr/share/java/
sudo mv mysql-connector-java-5.1.40/mysql-connector-java-5.1.40-bin.jar /usr/share/java/mysql-connector-java.jar
```

Install the MariaDB client on all the hosts:
```
[root@berlin yum.repos.d]# yum install -y MariaDB-client
```


Start the MariaDB server on amsterdam host: 
```
[root@amsterdam tmp]# sudo systemctl start mariadb
[root@amsterdam tmp]# service mariadb status
Redirecting to /bin/systemctl status mariadb.service
● mariadb.service - MariaDB 10.1.31 database server
   Loaded: loaded (/usr/lib/systemd/system/mariadb.service; enabled; vendor preset: disabled)
  Drop-In: /etc/systemd/system/mariadb.service.d
           └─migrated-from-my.cnf-settings.conf
   Active: active (running) since Fri 2018-03-16 08:40:22 UTC; 10s ago
     Docs: man:mysqld(8)
           https://mariadb.com/kb/en/library/systemd/
  Process: 2959 ExecStartPost=/bin/sh -c systemctl unset-environment _WSREP_START_POSITION (code=exited, status=0/SUCCESS)
  Process: 2839 ExecStartPre=/bin/sh -c [ ! -e /usr/bin/galera_recovery ] && VAR= ||   VAR=`/usr/bin/galera_recovery`; [ $? -eq 0 ]   && systemctl set-environment _WSREP_START_POSITION=$VAR || exit 1 (code=exited, status=0/SUCCESS)
  Process: 2837 ExecStartPre=/bin/sh -c systemctl unset-environment _WSREP_START_POSITION (code=exited, status=0/SUCCESS)
 Main PID: 2930 (mysqld)
   Status: "Taking your SQL requests now..."
   CGroup: /system.slice/mariadb.service
           └─2930 /usr/sbin/mysqld

Mar 16 08:40:21 amsterdam mysqld[2930]: 2018-03-16  8:40:21 139703096428800 [Warning] InnoDB: New log files created, LSN=1616908
Mar 16 08:40:21 amsterdam mysqld[2930]: 2018-03-16  8:40:21 139703096428800 [Note] InnoDB: 128 rollback segment(s) are active.
Mar 16 08:40:21 amsterdam mysqld[2930]: 2018-03-16  8:40:21 139703096428800 [Note] InnoDB: Waiting for purge to start
Mar 16 08:40:22 amsterdam mysqld[2930]: 2018-03-16  8:40:22 139703096428800 [Note] InnoDB:  Percona XtraDB (http://www.percona.com) ... 1616717
Mar 16 08:40:22 amsterdam mysqld[2930]: 2018-03-16  8:40:22 139697745524480 [Note] InnoDB: Dumping buffer pool(s) not yet started
Mar 16 08:40:22 amsterdam mysqld[2930]: 2018-03-16  8:40:22 139703096428800 [Note] Plugin 'FEEDBACK' is disabled.
Mar 16 08:40:22 amsterdam mysqld[2930]: 2018-03-16  8:40:22 139703096428800 [Note] Server socket created on IP: '::'.
Mar 16 08:40:22 amsterdam mysqld[2930]: 2018-03-16  8:40:22 139703096428800 [Note] /usr/sbin/mysqld: ready for connections.
Mar 16 08:40:22 amsterdam mysqld[2930]: Version: '10.1.31-MariaDB'  socket: '/var/lib/mysql/mysql.sock'  port: 3306  MariaDB Server
Mar 16 08:40:22 amsterdam systemd[1]: Started MariaDB 10.1.31 database server.
```

Secure it: 
```
[root@amsterdam tmp]# /usr/bin/mysql_secure_installation

NOTE: RUNNING ALL PARTS OF THIS SCRIPT IS RECOMMENDED FOR ALL MariaDB
      SERVERS IN PRODUCTION USE!  PLEASE READ EACH STEP CAREFULLY!

In order to log into MariaDB to secure it, we'll need the current
password for the root user.  If you've just installed MariaDB, and
you haven't set the root password yet, the password will be blank,
so you should just press enter here.

Enter current password for root (enter for none):
OK, successfully used password, moving on...

Setting the root password ensures that nobody can log into the MariaDB
root user without the proper authorisation.

Set root password? [Y/n] Y
New password:
Re-enter new password:
Password updated successfully!
Reloading privilege tables..
 ... Success!


By default, a MariaDB installation has an anonymous user, allowing anyone
to log into MariaDB without having to have a user account created for
them.  This is intended only for testing, and to make the installation
go a bit smoother.  You should remove them before moving into a
production environment.

Remove anonymous users? [Y/n] Y
 ... Success!

Normally, root should only be allowed to connect from 'localhost'.  This
ensures that someone cannot guess at the root password from the network.

Disallow root login remotely? [Y/n] n
 ... skipping.

By default, MariaDB comes with a database named 'test' that anyone can
access.  This is also intended only for testing, and should be removed
before moving into a production environment.

Remove test database and access to it? [Y/n] Y
 - Dropping test database...
 ... Success!
 - Removing privileges on test database...
 ... Success!

Reloading the privilege tables will ensure that all changes made so far
will take effect immediately.

Reload privilege tables now? [Y/n] Y
 ... Success!

Cleaning up...

All done!  If you've completed all of the above steps, your MariaDB
installation should now be secure.

Thanks for using MariaDB!
```

Creating databases:
```
```



Creating databases:
```
[root@amsterdam tmp]# mysql -u root -p
Enter password:
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 11
Server version: 10.1.31-MariaDB MariaDB Server

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
+--------------------+
3 rows in set (0.00 sec)

MariaDB [(none)]>
MariaDB [(none)]> create database scm DEFAULT CHARACTER SET utf8;
Query OK, 1 row affected (0.00 sec)

MariaDB [(none)]> create database rman DEFAULT CHARACTER SET utf8;
Query OK, 1 row affected (0.00 sec)

MariaDB [(none)]> create database hive DEFAULT CHARACTER SET utf8;
Query OK, 1 row affected (0.00 sec)

MariaDB [(none)]> create database oozie DEFAULT CHARACTER SET utf8;
Query OK, 1 row affected (0.00 sec)

MariaDB [(none)]> create database hue DEFAULT CHARACTER SET utf8;
Query OK, 1 row affected (0.00 sec)

MariaDB [(none)]> show databasese;
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MariaDB server version for the right syntax to use near 'databasese' at line 1
MariaDB [(none)]> show databases;
+--------------------+
| Database           |
+--------------------+
| hive               |
| hue                |
| information_schema |
| mysql              |
| oozie              |
| performance_schema |
| rman               |
| scm                |
+--------------------+
8 rows in set (0.00 sec)
```

Finally granting the access (for scm will be done after): 
```
MariaDB [(none)]> grant all on rman.* to 'rman' IDENTIFIED BY 'rman_password';
Query OK, 0 rows affected (0.00 sec)

MariaDB [(none)]> grant all on hive.* to 'hive' IDENTIFIED BY 'hive_password';
Query OK, 0 rows affected (0.00 sec)

MariaDB [(none)]> grant all on oozie.* to 'oozie' IDENTIFIED BY 'oozie_password';
Query OK, 0 rows affected (0.00 sec)

MariaDB [(none)]> grant all on hue.* to 'hue' IDENTIFIED BY 'hue_password';     Query OK, 0 rows affected (0.00 sec)

```
