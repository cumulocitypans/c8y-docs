---
weight: 60
title: Administration and configuration
layout: redirect
---

### Unlocking the tenant admin user

The tenant admin user could be locked if incorrect credentials are passed during login into UI, REST API or MQTT. 

<img src="/guides/images/edge/edge-tenant-lock.png" name="Locked user" style="width:50%;"/>

To unlock the tenant admin user, perform the following steps:

1. Login as sysadmin user (password= sysadmin-pass).
1. In the Administration application, navigate to the **Users** page and open the tenant admin user.
1. Activate the user account by switching the toggle next to the username to **Enabled** and save your settings.

### Configuring email server and password template settings

To configure the "reset password" template and email server settings, perform the following steps:

1. Log into the management tenant using *https://&#60;Edge&#95;VM&#95;IP&#95;Address>/apps/administration/index.html#/configuration*.
	* User: management/edgeadmin 
	* Password: Will be the same as the Edge tenant admin password provided in the post-installation execution
<br>
2. Update the email server details and templates following the instructions in [Administration > Changing settings> Configuration settings](/guides/users-guide/administration/#config-platform) in the User guide.


### Increasing the system performance

If the system performance is slow, the memory should be increased. First, increase the memory of the VM. This is done by stopping the VM and increasing its memory.

<img src="/guides/images/edge/edge-vm-increasing-memory.png" name="Increasing memory"/>

Increasing the VM memory should be followed by a JVM memory increase. 

This is done by starting the VM (follow the steps described in the Installation section). Log into VM, open the file */usr/share/cumulocity-core-karaf/bin/setenv*  and edit it as described below. The parameter is the following, default size is 1024.

	export JAVA_MAX_MEM=1024M # Maximum memory for the JVM

After increasing the size, restart Karaf by executing:

```shell
# service cumulocity-core-karaf stop
```

and

```shell
# service cumulocity-core-karaf start
```

Use the following command to check the JVM process of Karaf:

```shell
# ps aux | grep karaf
```

Sample output:

```shell
[root@server ~]# ps aux | grep karaf
	karaf     1525 44.1 15.2 3890280 618920 ?      Sl   09:56   2:21 /usr/java/default/bin/java -XX:+UseConcMarkSweepGC -Djava.rmi.server.hostname=127.0.0.1 -Djava.rmi.server.useLocalHostname=true -Dcom.sun.management.jmxremote -Dcom.sun.management.jmxremote.port=8199 -Dcom.sun.management.jmxremote.authenticate=false -Dcom.sun.management.jmxremote.ssl=false -server -Xms235M -Xmx1024M -XX:PermSize=16M -XX:MaxPermSize=512M -Dcom.sun.management.jmxremote -XX:+UseCompressedOops -XX:+UseParNewGC -XX:+UseConcMarkSweepGC 
	(rest of output trimmed)
	```

If Karaf is not stopped by executing `service cumulocity-core-karaf stop` you can search for the PID (process ID) with `command ps aux | grep karaf` and stop it by executing:

```shell	
# kill -9 <PID>
```

In the example above, the PID is 1525.

### Increasing the MQTT message size

By default, the max size for one MQTT message is 8192 bytes(8KB).

To increase the MQTT message size, add the property “mqtt.max.message.size” 
in */etc/cumulocity/cumulocity-core.properties*.

Example:

To set the message size to 16KB, set “mqtt.max.message.size=16384”.


After increasing the size, restart Karaf by executing:

```shell
# service cumulocity-core-karaf restart
```


### Log rotation 

Currently, there are two ways of configuring the log rotation for components.
<br>

**Under /usr/share/cumulocity-core-karaf/etc/ in org.ops4j.pax.logging.cfg file**

This configuration is done via configuring the RollingFileAppender provided by Log4J. 

The components for which log rotation is configured are as follows:

|Component|Log file location|Log file rotation|Max file size|Max backup index|
|:---|:---|:---|:---|:---|
|Karaf|${karaf.data}/log/error.log|Daily|50 MB|14|
|MQTT|${karaf.data}/log/mqtt.log|Daily|50 MB|14|
|Access|${karaf.data}/log/access.log|Daily|50 MB|14|
|DataBroker|${karaf.data}/log/databroker.log|Daily|50 MB|14|
 
<br>
**Under /etc/ configured via logrotate.conf and config files under /etc/logrotate.d**
 
The components for which log rotation is configured are as follows:
 
|Component|Log file location|Log file rotation|Max file size|Max backup index|
|:---|:---|:---|:---|:---|
|MongoDB|/var/log/mongodb/*.log|Daily|50 MB|14|
|NginX|/var/log/nginx/*.log|Daily|50 MB|14|
|Apama|/opt/softwareag/cumulocity-apama-rules/deploy/logs/*.log|Daily|50 MB|14|

Configuration can be altered by using daily/weekly/monthly and specifying the corresponding rotate count.

For microservices, there currently is no specific log rotation configured.

### Time synchronization

For many use cases, and especially when using APAMA, time synchronization must be available, i.e. the time inside the VM must be synchronized with the time of the host OS and with devices sending data.

Out of the box, for VMWare-based installations, vmtools is responsible for time synchronization with the host OS. For VirtualBox-based installations, VirtualBox guest additions is responsible. 

Additionally, chrony or ntp services can be configured by end users based on their time synchronization needs. Refer to the respective documentation for the configuration of these services. These services are by default stopped and disabled in Edge and can be enabled by standard commands.