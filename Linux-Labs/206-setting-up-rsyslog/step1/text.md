Your team has determined that they need to centralize logging in the environment. This is a Secure Technical Implementation Guide (STIG) for government systems. But, in your case, it's just a good practice and your team has been losing remediation time by not being able to see logs on systems until after the systems are back up. 

Your management has been coming around talking about MTTR and MTTD. You don't know what that means, but you know that getting logs to a central place will help make it better and management will leave you alone.

Verify that rsyslog is installed and running on both systems.

Configure rsyslog on controlplane to capture UDP on the default port 514.

Verify that rsyslog is listening on UDP port 514.

Configure rsyslog on node01 to send logs over UDP to controlplane

Verify that the logs are sending data from node01 to controlplane.

<br>

### Solution


Verify that rsyslog is installed and running on both systems.

```plain
dpkg -l | grep -i rsyslog
```

```plain
ssh node01 'dpkg -l | grep -i rsyslog'
```

```plain
systemctl status rsyslog
```

```plain
ssh node01 'systemctl status rsyslog'
```

Configure rsyslog on controlplane to capture UDP on the default port 514.

```plain
vi /etc/rsyslog.conf
```

Uncomment the following two lines

```plain
module(load="imudp")
input(type="imudp" port="514")
```

Hit esc :wq to write and quit

You know that systems do not take configuration file changes without a restart of the service, so restart rsyslog

```plain
systemctl restart rsyslog
```

Verify that your system is listening on port 514 for UDP traffic.

```plain
ss -ntulp | grep 514
```

ssh to node01

```plain
ssh node01
```

Configure the rsyslog daemon on node01

```plain
vi /etc/rsyslog.conf
```

Add the following line at the bottom of the file.

```plain
*.* @controlplane:514
```
Restart the service

```plain
systemctl restart rsyslog
```

Exit back to controlplane node

```plain
exit
```

Verify that the node01 system logs are being pushed over to controlplane

```plain
tail -f /var/log/syslog
```

You are ready to head to the next part of the lab.


