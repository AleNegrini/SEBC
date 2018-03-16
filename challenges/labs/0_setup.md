# Challenge Setup 

## Cluster information
The servers belonging to the cluster have been provisioned by Google Cloud Platform:
* __Region__: North-America (us-east1-b)
* __OS__ : Centos 7
* __Instance type__ : n1-highmem-2 instance (i.e. 2vCores and 13GB RAM)
* __Google Cloud Machine Image__ : Centos 7 x86_64 built on 20180227

Getting the list of the machines: 
```
[root@amsterdam ~]# getent ahosts
10.142.0.2      amsterdam.c.sebc-pre-challenges.internal amsterdam
10.142.0.6      berlin.c.sebc-pre-challenges.internal berlin
10.142.0.5      london.c.sebc-pre-challenges.internal london
10.142.0.3      milan.c.sebc-pre-challenges.internal milan
10.142.0.4      paris.c.sebc-pre-challenges.internal paris
```



All the OS are running with `CentOS 7` as OS.

My first node will be: 
```
10.142.0.2      amsterdam.c.sebc-pre-challenges.internal amsterdam
```
for the entire challenge. 

My second node will be: 
```
10.142.0.6      berlin.c.sebc-pre-challenges.internal berlin
```
for the entire challenge. 

Getting file system capacity on the first node: 
```
[root@amsterdam ~]# df -h
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1        50G  1.5G   49G   3% /
devtmpfs        6.3G     0  6.3G   0% /dev
tmpfs           6.3G     0  6.3G   0% /dev/shm
tmpfs           6.3G  8.4M  6.3G   1% /run
tmpfs           6.3G     0  6.3G   0% /sys/fs/cgroup
tmpfs           1.3G     0  1.3G   0% /run/user/0
```

List the command and output for (launched on all the hosts and output is the same on all the hosts):
```
[root@amsterdam ~]# yum repolist enabled
Loaded plugins: fastestmirror
Loading mirror speeds from cached hostfile
 * base: mirror.wdc1.us.leaseweb.net
 * epel: mirror.us.leaseweb.net
 * extras: mirror.rackspace.com
 * updates: mirrors.centos.webair.com
repo id              repo name                                 status
base/7/x86_64        CentOS-7 - Base                            9,591
epel/x86_64          Extra Packages for Enterprise Linux 7 - x 12,401
extras/7/x86_64      CentOS-7 - Extras                            436
google-cloud-compute Google Cloud Compute                           9
google-cloud-sdk     Google Cloud SDK                             425
updates/7/x86_64     CentOS-7 - Updates                         2,407
repolist: 25,269
```

On all the hosts, create the users: 
```
[root@amsterdam ~]# useradd -u 2800 hilary
[root@amsterdam ~]# useradd -u 2900 anupam
```

On all the hosts, create the groups: 
```
[root@amsterdam ~]# groupadd analytics
[root@amsterdam ~]# groupadd datasci
```

On all the hosts, make the assignments user-group:
```
[root@amsterdam ~]# usermod -a -G analytics anupam
[root@amsterdam ~]# usermod -a -G datasci hilary
```

On all the hosts, cat the `/etc/passwd` file: 
```
[root@amsterdam ~]# cat /etc/passwd | grep hilary
hilary:x:2800:2800::/home/hilary:/bin/bash
[root@amsterdam ~]# cat /etc/passwd | grep anupam
anupam:x:2900:2900::/home/anupam:/bin/bash
```
Getting the same result from all the hosts.

On all the hosts, cat the `/etc/group` file:
```
[root@amsterdam ~]# cat /etc/group | grep analytics
analytics:x:2901:anupam
[root@amsterdam ~]# cat /etc/group | grep datasci
datasci:x:2902:hilary
```
Getting the same result from all the hosts. 

Creating password for the users (command launched on all the hosts):
```
[root@amsterdam ~]# passwd hilary
Changing password for user hilary.
New password:
BAD PASSWORD: The password fails the dictionary check - it is based on a dictionary word
Retype new password:
passwd: all authentication tokens updated successfully.
[root@amsterdam ~]# passwd anupam
Changing password for user anupam.
New password:
BAD PASSWORD: The password fails the dictionary check - it is based on a dictionary word
Retype new password:
passwd: all authentication tokens updated successfully.
```


