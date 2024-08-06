You are a new system administrator at a company. You've been tasked with finding out information about a set of servers that has very little to no documentation on it.

Check kernel and package info on the system.

Echo the number of kernel versions that are stored on this system into /root/kernel.

Find specific versions of the software that the security team has been asking about, specifically ssh server and client.

<br>

### Solution
<details>
<summary>Solution</summary>
Check all the kernel information.

```plain
uname -a
```

Check for old versions of the kernel that are on the system.

```plain
ls /boot/vm*
```

Echo the number of versions into /root/kernel

```
echo 1 > /root/kernel
```

Next we will check how many packages are on the system.

```plain
dpkg -l | wc -l
```

What is the version of ssh on this system? Server and client.

```plain
dpkg -l | grep -i ssh
```

client is named openssh-client

server is named openssh-server

</details>