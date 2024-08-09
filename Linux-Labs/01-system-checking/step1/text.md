You are a new system administrator at a company. You've been tasked with finding out information about a set of servers that has very little to no documentation on it. You find yourself at a command prompt and need to find out what type of system you are working on.

What is the release and version of the system? 
- Ubuntu 20.04.5 LTS

What is the kernel version?
- 5.4.0-131-generic

How long has the system been up, and how was its kernel called as GRUB booted it?
- up 29 min
- BOOT_IMAGE=/boot/vmlinuz-5.4.0-131-generic root=LABEL=cloudimg-rootfs ro console=tty1 console=ttyS0

Use the Solution to follow along and look around a new Linux system for the first time.


### Solution

#### Check release
First we check what version of Linux we're on.

```plain
cat /etc/*release
```
- displays the contents of any files in the `/etc` directory that have "release" in their name
	- `lsb_release -a` is an alternative approach
	- `hostnamectl` systemd alternative, will show distro as well
	- `/proc/version` will have this info as well

#### Check kernel version
Next we check the kernel version.

```plain
uname -r
```
- `uname -r` only throws kernel version, `uname -a` will give more information, including type and platform, hostname, kernel release date


#### System's uptime
Next we might want to know how long the system has been up.

```plain
uptime
```
 - Command `uptime` gives us information about how long the system has been running, the current time, the number of users currently logged in, and the system load averages for the past 1, 5, and 15 minutes.
 - `w` is similar with user list
 - `/proc/uptime` file has the info as well


#### Boot parameters
Next we might want to see how the system booted and what kernel parameters were passed when the system was started.

```plain
cat /proc/cmdline
```

- displays the kernel command line parameters that were used when the system was booted
	- `dmesg | grep "command line"` is a valid alternative
	- `journalctl -b | grep "kernel: Command line:"` systemd alternative, works as well
