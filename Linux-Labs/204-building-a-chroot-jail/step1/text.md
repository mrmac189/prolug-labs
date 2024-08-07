Your team is planning on building a bastion system. You've read that the first part of properly bastioning systems is to jail, or lock users down. You have decided to build a jail and test functionality.

Build a jail at `/var/chroot/`.

Add basic framework to the jail so that you can populate it with functionality.

Change your root to /var/chroot and see what functionality you have.


<br>

### Solution


Create the chroot filesystem.

```plain
mkdir /var/chroot
```

Create the directory structure of the jail.

```plain
mkdir -p /var/chroot/{bin,lib64,dev,etc,home,usr/bin,lib/x86_64-linux-gnu}
```

Check the directories have been created.

```plain
ls -l /var/chroot
```

What directories do you see? Is there anything about these directories that you know about that would make sense to give a user?

Move in the minimum executibles for chroot to work properly.

```plain
cp /usr/bin/bash /var/chroot/bin/bash
```

The binary cannot work properly without the link libraries. Copy those in to get basic bash shell functionality.

```plain
for package in $(ldd /bin/bash | awk '{print $(NF -1)}'); do cp $package /var/chroot/$package; done
```

You can ignore the error about stat-ing the one file linux-vdso.so.1 it won't affect the rest of the lab.

Once you've done this you can jail your user and see what functionality you have in the jail.

Check your current bash process

```plain
echo $$
```

Jail your user in /var/chroot and see what functionality you have.

```plain
chroot /var/chroot
```

Check your current bash process

```plain
echo $$
```

If they're different you're in a jailed bash environment now.

Try any commands you know in Linux, what has happened to your user? Where are your commands at? can you use uptime? ping?

Spend time getting familiar with jails and [chroot](https://en.wikipedia.org/wiki/Chroot)

Exit the jail

```plain
exit
```

Perform some system commands to make sure you've left the jail. How did your command prompt change when you were jailed? Why do you think that is?

```plain
ping -c 1 www.google.com
```

Hit submit to move onto the next part of the lab.

