# Kerberize the cluster

Cluster has been kerberized using as master the host `berlin`.

Created the principle `cloudera-scm@ALENEGRINI.NL` as the privileged principal:
```
[root@berlin ~]# kinit cloudera-scm
Password for cloudera-scm@ALENEGRINI.NL:
[root@berlin ~]# klist
Ticket cache: FILE:/tmp/krb5cc_0
Default principal: cloudera-scm@ALENEGRINI.NL

Valid starting       Expires              Service principal
03/16/2018 10:23:37  03/17/2018 10:23:37  krbtgt/ALENEGRINI.NL@ALENEGRINI.NL
        renew until 03/23/2018 10:23:37
[root@berlin ~]# klist -e -f
Ticket cache: FILE:/tmp/krb5cc_0
Default principal: cloudera-scm@ALENEGRINI.NL

Valid starting       Expires              Service principal
03/16/2018 10:23:37  03/17/2018 10:23:37  krbtgt/ALENEGRINI.NL@ALENEGRINI.NL
        renew until 03/23/2018 10:23:37, Flags: FRI
        Etype (skey, tkt): aes256-cts-hmac-sha1-96, aes256-cts-hmac-sha1-96
```

Creating principle for `hilary` and `anupam`:
```
[root@berlin ~]# kadmin.local
Authenticating as principal root/admin@ALENEGRINI.NL with password.
kadmin.local:  addprinc hilary@ALENEGRINI.NL
WARNING: no policy specified for hilary@ALENEGRINI.NL; defaulting to no policy
Enter password for principal "hilary@ALENEGRINI.NL":
Re-enter password for principal "hilary@ALENEGRINI.NL":
Principal "hilary@ALENEGRINI.NL" created.
kadmin.local:  addprinc anupam@ALENEGRINI.NL
WARNING: no policy specified for anupam@ALENEGRINI.NL; defaulting to no policy
Enter password for principal "anupam@ALENEGRINI.NL":
Re-enter password for principal "anupam@ALENEGRINI.NL":
Principal "anupam@ALENEGRINI.NL" created.
```

Testing `hilary` principle from a client host: 
```
[root@london ~]# kinit hilary
Password for hilary@ALENEGRINI.NL:
[root@london ~]# klist -e -f
Ticket cache: FILE:/tmp/krb5cc_0
Default principal: hilary@ALENEGRINI.NL

Valid starting       Expires              Service principal
03/16/2018 10:28:12  03/17/2018 10:28:12  krbtgt/ALENEGRINI.NL@ALENEGRINI.NL
        renew until 03/23/2018 10:28:12, Flags: FRI
        Etype (skey, tkt): aes256-cts-hmac-sha1-96, aes256-cts-hmac-sha1-96
```

Testing `anupam` principle from a client host: 
```
[root@london ~]# kinit anupam
Password for anupam@ALENEGRINI.NL:
[root@london ~]# klist -e -f
Ticket cache: FILE:/tmp/krb5cc_0
Default principal: anupam@ALENEGRINI.NL

Valid starting       Expires              Service principal
03/16/2018 10:29:19  03/17/2018 10:29:19  krbtgt/ALENEGRINI.NL@ALENEGRINI.NL
        renew until 03/23/2018 10:29:19, Flags: FRI
        Etype (skey, tkt): aes256-cts-hmac-sha1-96, aes256-cts-hmac-sha1-96
```

And finally, testing what HDFS is "seeing":
```
[root@london ~]# hdfs groups anupam
anupam : anupam analytics
[root@london ~]# hdfs groups hilary
hilary : hilary datasci
```

I then proceeded with the Cloudera Manager integration. 