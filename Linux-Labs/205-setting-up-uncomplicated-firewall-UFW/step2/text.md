So far you've enabled UFW and verified that you could see the open ports that are allowed to be connected to on your host.

Setup a web server (apache2) on node01.

Verify from controlplane that you cannot connect on port 80 to node01.

Allow apache2 (port 80) to be exposed through the UFW.

Verify from controlplane that you can now connect on port 80 to node01.

<br>

### Solution


Install the apache2 web server and verify it is running.

```plain
apt -y install apache2
```

```plain
ss -ntulp | grep -i apache2
lsof -i :80
```

Exit back to controlplane and verify that you cannot connect to apache on node01

```plain
exit
```

```plain
timeout 5 curl node01:80
```

Why do you think you were unable to connect?

Connect back to node01 and check your list of apps in UFW

```plain
ssh node01
```

```plain
ufw app list 
```

Is this different than what you saw before? Why do you think that is?

Check for any differences between the apps that were added.

```plain
ufw app info Apache
ufw app info "Apache Full"
ufw app info "Apache Secure"
```

What differences do you see in these? Why might it matter?

Allow apache to be exposed through the firewall

```plain
ufw allow Apache
```

Exit back to controlplane and verify that you can connect to apache on node01

```plain
exit
```

```plain
curl node01:80
timeout 3 curl node01 | grep "Apache2 Ubuntu Default Page"
```

What did you see when it connected?

Was it the default apache web page?

