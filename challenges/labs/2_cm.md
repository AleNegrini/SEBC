# Cloudera Manager installation

Cloudera Manager will be installed on berlin host (my second host).
Before installing Cloudera Manager and MySQL, I made sure to prepare the OS according to all the OS pre-requisites:
* Swappiness set to 1
* SELinux disabled
* IPv6 disabled
* Firewall services disabled
* Transparent Hugepage disabled
* nscd service installed and started
* ntpd service installed, started and syncronized
* for what concerns ulimits, according to the documentation, they will be automatically set by Cloudera Manager during its installation

Download the repo file from cloudera archive: 
```
[root@berlin yum.repos.d]# wget https://archive.cloudera.com/cm5/redhat/7/x86_64/cm/cloudera-manager.repo
--2018-03-16 08:57:42--  https://archive.cloudera.com/cm5/redhat/7/x86_64/cm/cloudera-manager.repo
Resolving archive.cloudera.com (archive.cloudera.com)... 151.101.32.167
Connecting to archive.cloudera.com (archive.cloudera.com)|151.101.32.167|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 290
Saving to: ‘cloudera-manager.repo’

100%[======================================>] 290         --.-K/s   in 0s

2018-03-16 08:57:42 (64.2 MB/s) - ‘cloudera-manager.repo’ saved [290/290]

[root@berlin yum.repos.d]# ls /etc/yum.repos.d/
CentOS-Base.repo       CentOS-Media.repo      epel.repo
CentOS-CR.repo         CentOS-Sources.repo    epel-testing.repo
CentOS-Debuginfo.repo  CentOS-Vault.repo      google-cloud.repo
CentOS-fasttrack.repo  cloudera-manager.repo  mariadb.repo
```

Modify the cloudera-manager.repo file in order to install the 5.13.x (latest) version: 
```
[root@berlin yum.repos.d]# cat cloudera-manager.repo
[cloudera-manager]
# Packages for Cloudera Manager, Version 5, on RedHat or CentOS 7 x86_64        
name=Cloudera Manager
baseurl=https://archive.cloudera.com/cm5/redhat/7/x86_64/cm/5.13/
gpgkey =https://archive.cloudera.com/cm5/redhat/7/x86_64/cm/RPM-GPG-KEY-cloudera
gpgcheck = 1
```

Reposync: 
```
[root@berlin yum.repos.d]# reposync -r cloudera-manager
cloudera-manager                                         |  951 B     00:00
cloudera-manager/primary                                   | 4.3 kB   00:00
warning: /etc/yum.repos.d/cloudera-manager/RPMS/x86_64/cloudera-manager-agent-5.13.2-1.cm5132.p0.6.el7.x86_64.rpm: Header V4 DSA/SHA1 Signature, key ID e8f86acd: NOKEY
Public key for cloudera-manager-agent-5.13.2-1.cm5132.p0.6.el7.x86_64.rpm is not installed
(1/7): cloudera-manager-agent-5.13.2-1.cm5132.p0.6.el7.x86 | 9.4 MB   00:00
(2/7): cloudera-manager-server-5.13.2-1.cm5132.p0.6.el7.x8 | 8.5 kB   00:00
(3/7): cloudera-manager-server-db-2-5.13.2-1.cm5132.p0.6.e |  10 kB   00:00
(4/7): enterprise-debuginfo-5.13.2-1.cm5132.p0.6.el7.x86_6 |  29 MB   00:01
(5/7): jdk-6u31-linux-amd64.rpm                            |  68 MB   00:01
(6/7): oracle-j2sdk1.7-1.7.0+update67-1.x86_64.rpm         | 135 MB   00:02
(7/7): cloudera-manager-daemons-5.13.2-1.cm5132.p0.6.el7.x | 665 MB   00:31
```

Now install it: 
```
[root@berlin yum.repos.d]# sudo yum install cloudera-manager-daemons cloudera-manager-server
Loaded plugins: fastestmirror
Loading mirror speeds from cached hostfile
 * base: mirror.wdc1.us.leaseweb.net
 * epel: reflector.westga.edu
 * extras: mirror.rackspace.com
 * updates: linux.cc.lehigh.edu
Resolving Dependencies
--> Running transaction check
---> Package cloudera-manager-daemons.x86_64 0:5.13.2-1.cm5132.p0.6.el7 will be installed
---> Package cloudera-manager-server.x86_64 0:5.13.2-1.cm5132.p0.6.el7 will be installed
--> Finished Dependency Resolution

Dependencies Resolved

================================================================================
 Package                 Arch   Version                  Repository        Size
================================================================================
Installing:
 cloudera-manager-daemons
                         x86_64 5.13.2-1.cm5132.p0.6.el7 cloudera-manager 665 M
 cloudera-manager-server x86_64 5.13.2-1.cm5132.p0.6.el7 cloudera-manager 8.5 k

Transaction Summary
================================================================================
Install  2 Packages

Total download size: 665 M
Installed size: 843 M
Is this ok [y/d/N]: y
Downloading packages:
warning: /var/cache/yum/x86_64/7/cloudera-manager/packages/cloudera-manager-server-5.13.2-1.cm5132.p0.6.el7.x86_64.rpm: Header V4 DSA/SHA1 Signature, key ID e8f86acd: NOKEY
Public key for cloudera-manager-server-5.13.2-1.cm5132.p0.6.el7.x86_64.rpm is not installed
(1/2): cloudera-manager-server-5.13.2-1.cm5132.p0.6.el7.x8 | 8.5 kB   00:00
(2/2): cloudera-manager-daemons-5.13.2-1.cm5132.p0.6.el7.x | 665 MB   00:19
--------------------------------------------------------------------------------
Total                                               33 MB/s | 665 MB  00:19
Retrieving key from https://archive.cloudera.com/cm5/redhat/7/x86_64/cm/RPM-GPG-KEY-cloudera
Importing GPG key 0xE8F86ACD:
 Userid     : "Yum Maintainer <webmaster@cloudera.com>"
 Fingerprint: 5f14 d39e f068 1aca 6f04 4a43 f90c 0d8f e8f8 6acd
 From       : https://archive.cloudera.com/cm5/redhat/7/x86_64/cm/RPM-GPG-KEY-cloudera
Is this ok [y/N]: y
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Installing : cloudera-manager-daemons-5.13.2-1.cm5132.p0.6.el7.x86_64     1/2
  Installing : cloudera-manager-server-5.13.2-1.cm5132.p0.6.el7.x86_64      2/2
  Verifying  : cloudera-manager-server-5.13.2-1.cm5132.p0.6.el7.x86_64      1/2
  Verifying  : cloudera-manager-daemons-5.13.2-1.cm5132.p0.6.el7.x86_64     2/2

Installed:
  cloudera-manager-daemons.x86_64 0:5.13.2-1.cm5132.p0.6.el7
  cloudera-manager-server.x86_64 0:5.13.2-1.cm5132.p0.6.el7

Complete!
```


Before run Cloudera Manager I should prepare the scm database (on the amsterdam host): 
```
MariaDB [(none)]>  GRANT ALL on scm.* TO 'root'@'berlin.c.sebc-pre-challenges.internal' IDENTIFIED BY '123qwe..';
Query OK, 0 rows affected (0.00 sec)
```

Install JDK1.7:
```
[root@berlin yum.repos.d]# sudo yum install oracle-j2sdk1.7
```

```
[root@berlin yum.repos.d]# /usr/share/cmf/schema/scm_prepare_database.sh mysql -hamsterdam.c.sebc-pre-challenges.internal scm root 123qwe..
JAVA_HOME=/usr/java/jdk1.7.0_67-cloudera
Verifying that we can write to /etc/cloudera-scm-server
Creating SCM configuration file in /etc/cloudera-scm-server
Executing:  /usr/java/jdk1.7.0_67-cloudera/bin/java -cp /usr/share/java/mysql-connector-java.jar:/usr/share/java/oracle-connector-java.jar:/usr/share/cmf/schema/../lib/* com.cloudera.enterprise.dbutil.DbCommandExecutor /etc/cloudera-scm-server/db.properties com.cloudera.cmf.db.
[                          main] DbCommandExecutor              INFO  Successfully connected to database.
All done, your SCM database is configured correctly!
```

Start the CM server: 
```
[root@berlin yum.repos.d]# service cloudera-scm-server start
Starting cloudera-scm-server (via systemctl):              [  OK  ]
```

Check in the /var/log/cloudera-scm-server/cloudera-scm-server.log file if the web server started (Jetty server started):
```
[root@berlin yum.repos.d]# tail -10 /var/log/cloudera-scm-server/cloudera-scm-server.log
2018-03-16 09:12:25,496 INFO SearchRepositoryManager-0:com.cloudera.server.web.cmf.search.components.SearchRepositoryManager: Initializing SearchTemplateManager:2018-03-16T09:12:25.496Z
2018-03-16 09:12:25,571 INFO SearchRepositoryManager-0:com.cloudera.server.web.cmf.search.components.SearchRepositoryManager: Generating entities:2018-03-16T09:12:25.571Z
2018-03-16 09:12:25,628 INFO SearchRepositoryManager-0:com.cloudera.server.web.cmf.search.components.SearchRepositoryManager: Num entities:205
2018-03-16 09:12:25,629 INFO SearchRepositoryManager-0:com.cloudera.server.web.cmf.search.components.SearchRepositoryManager: Generating documents:2018-03-16T09:12:25.628Z
2018-03-16 09:12:25,708 INFO SearchRepositoryManager-0:com.cloudera.server.web.cmf.search.components.SearchRepositoryManager: Num docs:218
2018-03-16 09:12:25,710 INFO SearchRepositoryManager-0:com.cloudera.server.web.cmf.search.components.SearchRepositoryManager: Constructing repo:2018-03-16T09:12:25.710Z
2018-03-16 09:12:27,720 INFO SearchRepositoryManager-0:com.cloudera.server.web.cmf.search.components.SearchRepositoryManager: Finished constructing repo:2018-03-16T09:12:27.720Z
2018-03-16 09:12:28,407 INFO WebServerImpl:org.mortbay.log: jetty-6.1.26.cloudera.4
2018-03-16 09:12:28,408 INFO WebServerImpl:org.mortbay.log: Started SelectChannelConnector@0.0.0.0:7180
2018-03-16 09:12:28,408 INFO WebServerImpl:com.cloudera.server.cmf.WebServerImpl: Started Jetty server.
```

