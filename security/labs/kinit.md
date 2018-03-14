## After Kerberos installation: double checks

```
[root@amsterdam krb5kdc]# kinit cloudera-scm@HADOOP.COM
Password for cloudera-scm@HADOOP.COM:
[root@amsterdam krb5kdc]# klist
Ticket cache: FILE:/tmp/krb5cc_0
Default principal: cloudera-scm@HADOOP.COM

Valid starting       Expires              Service principal
03/14/2018 16:17:22  03/15/2018 16:17:22  krbtgt/HADOOP.COM@HADOOP.COM
        renew until 03/21/2018 16:17:22
[root@amsterdam krb5kdc]# klist -e -f
Ticket cache: FILE:/tmp/krb5cc_0
Default principal: cloudera-scm@HADOOP.COM

Valid starting       Expires              Service principal
03/14/2018 16:17:22  03/15/2018 16:17:22  krbtgt/HADOOP.COM@HADOOP.COM
        renew until 03/21/2018 16:17:22, Flags: FRI
        Etype (skey, tkt): arcfour-hmac, aes256-cts-hmac-sha1-96
```


In order to double check the Kerberos installation I tried to launch the following command in order to see that the user hdfs is not able to run commands any more: 
```
[hdfs@amsterdam krb5kdc]$ hdfs dfs -ls /
18/03/14 15:23:31 WARN security.UserGroupInformation: PriviledgedActionException as:hdfs (auth:KERBEROS) cause:javax.security.sasl.SaslException: GSS initiate failed [Caused by GSSException: No valid credentials provided (Mechanism level: Failed to find any Kerberos tgt)]
18/03/14 15:23:31 WARN ipc.Client: Exception encountered while connecting to the server : javax.security.sasl.SaslException: GSS initiate failed [Caused by GSSException: No valid credentials provided (Mechanism level: Failed to find any Kerberos tgt)]
18/03/14 15:23:31 WARN security.UserGroupInformation: PriviledgedActionException as:hdfs (auth:KERBEROS) cause:java.io.IOException: javax.security.sasl.SaslException: GSS initiate failed [Caused by GSSException: No valid credentials provided (Mechanism level: Failed to find any Kerberos tgt)]
18/03/14 15:23:31 WARN security.UserGroupInformation: PriviledgedActionException as:hdfs (auth:KERBEROS) cause:javax.security.sasl.SaslException: GSS initiate failed [Caused by GSSException: No valid credentials provided (Mechanism level: Failed to find any Kerberos tgt)]
18/03/14 15:23:31 WARN ipc.Client: Exception encountered while connecting to the server : javax.security.sasl.SaslException: GSS initiate failed [Caused by GSSException: No valid credentials provided (Mechanism level: Failed to find any Kerberos tgt)]
18/03/14 15:23:31 WARN security.UserGroupInformation: PriviledgedActionException as:hdfs (auth:KERBEROS) cause:java.io.IOException: javax.security.sasl.SaslException: GSS initiate failed [Caused by GSSException: No valid credentials provided (Mechanism level: Failed to find any Kerberos tgt)]
18/03/14 15:23:31 INFO retry.RetryInvocationHandler: Exception while invoking getFileInfo of class ClientNamenodeProtocolTranslatorPB over berlin.c.sebc-labs.internal/10.142.0.3:8020 after 1 fail over attempts. Trying to fail over immediately.
java.io.IOException: Failed on local exception: java.io.IOException: javax.security.sasl.SaslException: GSS initiate failed [Caused by GSSException: No valid credentials provided (Mechanism level: Failed to find any Kerberos tgt)]; Host Details : local host is: "amsterdam.c.sebc-labs.internal/10.142.0.2"; destination host is: "berlin.c.sebc-labs.internal":8020;
```

Adding a new principal (after having configured HDFS with the superuser from Cloudera Manager):
```
[root@amsterdam krb5kdc]# kadmin.local
Authenticating as principal root/admin@HADOOP.COM with password.
kadmin.local:  addprinc sebc@HADOOP.COM
WARNING: no policy specified for sebc@HADOOP.COM; defaulting to no policy
Enter password for principal "sebc@HADOOP.COM":
Re-enter password for principal "sebc@HADOOP.COM":
Principal "sebc@HADOOP.COM" created.
```

```
[root@amsterdam krb5kdc]# hdfs dfs -ls /
Found 6 items
drwxr-xr-x   - hdfs supergroup          0 2018-03-13 09:45 /AleNegrini
drwxrwxrwx   - hdfs supergroup          0 2018-03-13 10:37 /jconca
drwxr-xr-x   - hdfs supergroup          0 2018-03-13 13:01 /precious
drwxr-xr-x   - hdfs supergroup          0 2018-03-13 17:42 /results
drwxrwxrwt   - hdfs supergroup          0 2018-03-14 12:39 /tmp
drwxr-xr-x   - hdfs supergroup          0 2018-03-14 12:39 /user
```


