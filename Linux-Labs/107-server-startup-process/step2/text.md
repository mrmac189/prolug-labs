Now it's time to look at the running processes and evaluate how this server booted up.

Evaluate how long the server took to come up from the time the kernel was called.

Evaluate the startup process of the ssh daemon. How was it started? What are the dependencies.

List any failed services during the startup.

What exposed ports do you see and what software are listening on those ports?

<br>

### Solution



Let's start by looking at everything the kernel did from the time it was first called.

```plain
dmesg | more
```

What do you think the important pieces of the system startup are?

Can you find the ethernet and it's associated driver?

```plain
dmesg | grep -i eth
```

Can you verify that this has been loaded as a kernel module?

```plain
lsmod | grep -i virtio_net
```

What other important kernel modules might you find with lsmod?

Let's see how long the system took to come up to it's runtime target

```plain
systemd-analyze time
```

What was the startup time for your system, according to systemd? How long did it take to get the system ready?

Now lets look at how long each individual daemon took.

```plain
systemd-analyze blame
```

What is the order of this output? Is the output serial or are some of them started in parallel? How would you know?

Check if the ssh.service is running on this server.

```plain
systemctl status ssh.service
```

Is the ssh.service running on this server? Is it set to run on startup? What is the PID of the service? 

Is there another way you can check that the service is enabled on startup?

```plain
systemctl is-enabled ssh.service
```

Can you check where systemd looked and the file it used to start this service?

```plain
systemctl cat ssh.service
```

Check the dependency chain for how systemd started ssh.service as this server booted.

```plain
systemd-analyze critical-chain ssh.service
```

What if we wanted to see all the system services that systemd started? How might we do that?

```plain
systemctl list-unit-files --no-pager | grep -i enabled
```

What if you wanted to count them up?

```plain
systemctl list-unit-files --no-pager | grep -i enabled | nl
systemctl list-unit-files --no-pager | grep -i enabled | wc -l
```

What if you wanted to count the instances of state for all of the enabled services?

```plain
systemctl list-unit-files --no-pager | grep -i enabled | awk '{print $2}' | sort | uniq -c
```

Take that command apart and see what each piece is doing and showing you. Why might it be important to see the masked items?

What if we needed to know the version of sshd that is installed on our system? 

```plain
dpkg -l | grep -i ssh
```

What version of ssh client and server do you have on the system?

What path holds the configuration files for your ssh components?

```plain
ls -l /etc/ssh
```

What is the server and what is the client configurations? What are some of the other files in there?

