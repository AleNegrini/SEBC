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

These steps were then applied to all the hosts

