# Pre-Install

## Checking swappiness
The following commands have been launched on host called "Amsterdam" with root user
Check the actual value of __vm.swappiness__:
```
[root@amsterdam cloudera]# cat /proc/sys/vm/swappiness
30
```
Set temporarly it to 1:
```
[root@amsterdam cloudera]# sudo sysctl vm.swappiness=1
vm.swappiness = 1
```
Setting the swappiness permanently to 1 (robust to restarts):
```
[root@amsterdam cloudera] sudo vi /etc/sysctl.conf
+ vm.swappiness = 1 (added this line)
```
Double check the new __vm.swappiness__ value:
```
[root@amsterdam cloudera]# cat /proc/sys/vm/swappiness
1
```

## Disable SELinux
Disable SELinux:
```
[root@amsterdam cloudera] vi /etc/sysconfig/selinux
- SELINUX=enforcing (remove this line)
+ SELINUX=disabled (add this line)
```
Save and reboot the machine

## Disable IPv6
```
[root@amsterdam cloudera] vi /etc/sysctl.conf
+ net.ipv6.conf.all.disable_ipv6 = 1 (add this line)
```
Save and reboot the machine

## Ulimits checks
```
[cloudera@amsterdam ~]$ ulimit -a
core file size          (blocks, -c) 0
data seg size           (kbytes, -d) unlimited
scheduling priority             (-e) 0
file size               (blocks, -f) unlimited
pending signals                 (-i) 51398
max locked memory       (kbytes, -l) 64
max memory size         (kbytes, -m) unlimited
open files                      (-n) 1024
pipe size            (512 bytes, -p) 8
POSIX message queues     (bytes, -q) 819200
real-time priority              (-r) 0
stack size              (kbytes, -s) 8192
cpu time               (seconds, -t) unlimited
max user processes              (-u) 4096
virtual memory          (kbytes, -v) unlimited
file locks                      (-x) unlimited
```
From the documentation: "Cloudera Manager will fix this issue, but if you aren’t running Cloudera Manager, be aware of this fact. Cloudera Manager will not alter users’ limits outside of Hadoop’s default limits. Nevertheless, it is still beneficial to raise the global limits to 64k."

## Checking volumes
```
[root@amsterdam cloudera]# cat /etc/fstab

#
# /etc/fstab
# Created by anaconda on Wed Feb 28 02:33:04 2018
#
# Accessible filesystems, by reference, are maintained under '/dev/disk'
# See man pages fstab(5), findfs(8), mount(8) and/or blkid(8) for more info
#
UUID=f4da24c0-b90a-4ae1-9e81-7eebfe5c28d5 /                       xfs     defaults        0 0

[root@amsterdam cloudera]# df -h
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1        50G  1.6G   49G   4% /
devtmpfs        6.3G     0  6.3G   0% /dev
tmpfs           6.3G     0  6.3G   0% /dev/shm
tmpfs           6.3G  8.3M  6.3G   1% /run
tmpfs           6.3G     0  6.3G   0% /sys/fs/cgroup
tmpfs           1.3G     0  1.3G   0% /run/user/1004
```

## Disable Transparent Huge Page
Check the current setting: 
```
[root@amsterdam transparent_hugepage]# cat /sys/kernel/mm/transparent_hugepage/defrag
[always] madvise never
[root@amsterdam transparent_hugepage]# cat /sys/kernel/mm/transparent_hugepage/enabled
[always] madvise never

```
Disable Transparent Hugepage support (temporarly):
```
[root@amsterdam transparent_hugepage]# echo 'never' > /sys/kernel/mm/transparent_hugepage/defrag
[root@amsterdam transparent_hugepage]# echo 'never' > /sys/kernel/mm/transparent_hugepage/enabled
```
Permanently apply changes
```
add the following line to /etc/rc.d/rc.local file
echo never > /sys/kernel/mm/transparent_hugepage/defrag
echo never > /sys/kernel/mm/transparent_hugepage/enabled
```
Modify the permissions of the rc.local file:
```
chmod +x /etc/rc.d/rc.local
```
Double check that everything is ok:
```
[root@amsterdam transparent_hugepage]# cat /sys/kernel/mm/transparent_hugepage/enabled
always madvise [never]
[root@amsterdam transparent_hugepage]# cat /sys/kernel/mm/transparent_hugepage/defrag
always madvise [never]
```

## Network interface configuration
```
[root@amsterdam transparent_hugepage]# netstat -i
Kernel Interface table
Iface      MTU    RX-OK RX-ERR RX-DRP RX-OVR    TX-OK TX-ERR TX-DRP TX-OVR Flg
eth0      1460    17158      0      0 0         18683      0      0      0 BMRU
lo       65536        0      0      0 0             0      0      0      0 LRU
[root@amsterdam transparent_hugepage]# ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN qlen 1
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1460 qdisc mq state UP qlen 1000
    link/ether 42:01:0a:8e:00:02 brd ff:ff:ff:ff:ff:ff
    inet 10.142.0.2/32 brd 10.142.0.2 scope global dynamic eth0
       valid_lft 80565sec preferred_lft 80565sec
```

## Forward and Revers host lookups
### Getent command: forward and reverse lookups
```
[root@amsterdam transparent_hugepage]# getent ahosts
127.0.0.1       localhost localhost.localdomain localhost4 localhost4.localdomain4
127.0.0.1       localhost localhost.localdomain localhost6 localhost6.localdomain6
10.142.0.3      berlin.c.sebc-labs.internal berlin
10.142.0.4      london.c.sebc-labs.internal london
10.142.0.5      milan.c.sebc-labs.internal milan
10.142.0.6      paris.c.sebc-labs.internal paris
10.142.0.2      amsterdam.c.sebc-labs.internal amsterdam
169.254.169.254 metadata.google.internal
[root@amsterdam transparent_hugepage]# getent hosts berlin
10.142.0.3      berlin.c.sebc-labs.internal berlin
[root@amsterdam transparent_hugepage]# getent hosts berlin.c.sebc-labs.internal
10.142.0.3      berlin.c.sebc-labs.internal berlin
[root@amsterdam transparent_hugepage]# getent hosts milan
10.142.0.5      milan.c.sebc-labs.internal milan
[root@amsterdam transparent_hugepage]# getent hosts milan.c.sebc-labs.internal
10.142.0.5      milan.c.sebc-labs.internal milan
[root@amsterdam transparent_hugepage]# getent hosts london
10.142.0.4      london.c.sebc-labs.internal london
[root@amsterdam transparent_hugepage]# getent hosts london.c.sebc-labs.internal
10.142.0.4      london.c.sebc-labs.internal london
[root@amsterdam transparent_hugepage]# getent hosts paris
10.142.0.6      paris.c.sebc-labs.internal paris
[root@amsterdam transparent_hugepage]# getent hosts paris.c.sebc-labs.internal
10.142.0.6      paris.c.sebc-labs.internal paris
[root@amsterdam transparent_hugepage]# getent hosts amsterdam
::1             amsterdam localhost
[root@amsterdam transparent_hugepage]# getent hosts amsterdam.c.sebc-labs.internal
10.142.0.2      amsterdam.c.sebc-labs.internal amsterdam
[root@amsterdam transparent_hugepage]# getent hosts 10.142.0.3
10.142.0.3      berlin.c.sebc-labs.internal berlin
[root@amsterdam transparent_hugepage]# getent hosts 10.142.0.5
10.142.0.5      milan.c.sebc-labs.internal milan
[root@amsterdam transparent_hugepage]# getent hosts 10.142.0.4
10.142.0.4      london.c.sebc-labs.internal london
[root@amsterdam transparent_hugepage]# getent hosts 10.142.0.6
10.142.0.6      paris.c.sebc-labs.internal paris
[root@amsterdam transparent_hugepage]# getent hosts 10.142.0.2
10.142.0.2      amsterdam.c.sebc-labs.internal amsterdam
[root@amsterdam transparent_hugepage]#

```
### nslookup command: forward and reverse lookup
```
[root@amsterdam transparent_hugepage]# nslookup berlin.c.sebc-labs.internal
Server:         169.254.169.254
Address:        169.254.169.254#53

Non-authoritative answer:
Name:   berlin.c.sebc-labs.internal
Address: 10.142.0.3

[root@amsterdam transparent_hugepage]# nslookup amsterdam.c.sebc-labs.internal
Server:         169.254.169.254
Address:        169.254.169.254#53

Non-authoritative answer:
Name:   amsterdam.c.sebc-labs.internal
Address: 10.142.0.2

[root@amsterdam transparent_hugepage]# nslookup paris.c.sebc-labs.internal
Server:         169.254.169.254
Address:        169.254.169.254#53

Non-authoritative answer:
Name:   paris.c.sebc-labs.internal
Address: 10.142.0.4

[root@amsterdam transparent_hugepage]# nslookup milan.c.sebc-labs.internal
Server:         169.254.169.254
Address:        169.254.169.254#53

Non-authoritative answer:
Name:   milan.c.sebc-labs.internal
Address: 10.142.0.6

[root@amsterdam transparent_hugepage]# nslookup london.c.sebc-labs.internal
Server:         169.254.169.254
Address:        169.254.169.254#53

Non-authoritative answer:
Name:   london.c.sebc-labs.internal
Address: 10.142.0.5

[root@amsterdam transparent_hugepage]# nslookup 10.142.0.2
Server:         169.254.169.254
Address:        169.254.169.254#53

Non-authoritative answer:
2.0.142.10.in-addr.arpa name = amsterdam.c.sebc-labs.internal.

Authoritative answers can be found from:

[root@amsterdam transparent_hugepage]# nslookup 10.142.0.3
Server:         169.254.169.254
Address:        169.254.169.254#53

Non-authoritative answer:
3.0.142.10.in-addr.arpa name = berlin.c.sebc-labs.internal.

Authoritative answers can be found from:

[root@amsterdam transparent_hugepage]# nslookup 10.142.0.4
Server:         169.254.169.254
Address:        169.254.169.254#53

Non-authoritative answer:
4.0.142.10.in-addr.arpa name = paris.c.sebc-labs.internal.

Authoritative answers can be found from:

[root@amsterdam transparent_hugepage]# nslookup 10.142.0.5
Server:         169.254.169.254
Address:        169.254.169.254#53

Non-authoritative answer:
5.0.142.10.in-addr.arpa name = london.c.sebc-labs.internal.

Authoritative answers can be found from:

[root@amsterdam transparent_hugepage]# nslookup 10.142.0.6
Server:         169.254.169.254
Address:        169.254.169.254#53

Non-authoritative answer:
6.0.142.10.in-addr.arpa name = milan.c.sebc-labs.internal.

Authoritative answers can be found from:

```

## nscd
```
[root@amsterdam transparent_hugepage]# sudo yum install nscd
[root@amsterdam transparent_hugepage]# service nscd start
[root@amsterdam transparent_hugepage]# chkconfig nscd on
Note: Forwarding request to 'systemctl enable nscd.service'.
Created symlink from /etc/systemd/system/multi-user.target.wants/nscd.service to /usr/lib/systemd/system/nscd.service.
Created symlink from /etc/systemd/system/sockets.target.wants/nscd.socket to /usr/lib/systemd/system/nscd.socket.
```
Test it 
```
[root@amsterdam transparent_hugepage]# time nslookup milan
Server:         169.254.169.254
Address:        169.254.169.254#53

Non-authoritative answer:
Name:   milan.c.sebc-labs.internal
Address: 10.142.0.6


real    0m0.019s
user    0m0.005s
sys     0m0.005s
[root@amsterdam transparent_hugepage]# time nslookup milan
Server:         169.254.169.254
Address:        169.254.169.254#53

Non-authoritative answer:
Name:   milan.c.sebc-labs.internal
Address: 10.142.0.6


real    0m0.009s
user    0m0.004s
sys     0m0.004s
```


These steps were then applied to all the hosts
