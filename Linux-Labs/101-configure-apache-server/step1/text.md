Your team has determined they need a website to test deployments rapidly. You have been tasked with installing a web server on node01.

Deploy an apache2 webserver on node01.

Capture the version and installed apache2 packages for your records.

Verify that node01 is listening on port 80.

Verify that the web page is working.

<br>

### Solution


Connect to node01

```plain
ssh node01
```

Verify there is no apache2 package

```plain
dpkg -l | grep -i apache2
systemctl | grep -i apache2
```

Deploy the apache2 webserver package

```plain
apt -y install apache2
```

Verfiy the version of software

```plain
dpkg -l | grep -i apache2
```

Verify that the server is running, set to run on reboot, and it working on the default ports.

```plain
systemctl status apache2.service --no-pager
lsof -i :80
ss -ntulp | grep :80
```

What are the names of the users that kicked off this process? Why might it be important to note this?

Further verify that the firewall isn't running to complicate things

```plain
ufw status
```

Should see this disabled.

Let's go back to controlplane 

```plain
exit
```

Make sure you can see the default webpage

```plain
curl node01:80
```
 
Did you see the default webpage? Ok, you've set up the first part, let's see what else out team has for us in the next part.

