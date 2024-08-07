You are a new system administrator at a company. You've been tasked with finding out information about a set of servers that has very little to no documentation on it. You find yourself at a command prompt and need to find out what type of system you are working on.

What is the release and version of the system?

What is the kernel version?

How long has the system been up, and how was its kernel called as GRUB booted it?

Use the Solution to follow along and look around a new Linux system for the first time.

<br>

### Solution


First we check what version of Linux we're on.

```plain
cat /etc/*release
```

Next we check the kernel version.

```plain
uname -r
```

Next we might want to know how long the system has been up.

```plain
uptime
```

Next we might want to see how the system booted and what kernel parameters were passed when the system was started.

```plain
cat /proc/cmdline
```


