The baduser is supposed to have the permissions they're trying to sudo to. So lets give them those permissions

Give sudo permissions to the user baduser. 

<br>

### Solution
<details>
<summary>Solution</summary>
There are many ways to give sudo permissions. You can add them directly to the /etc/sudoers file. You can add them to their own files in /etc/sudoers.d/ directory. We're just going to inspect the current sudoers and then put the user in a group that was already set up to give them sudoers permissions..

Inspect sudoers file.
```plain
cat /etc/sudoers
```

Give this file a quick read: Which groups does it say have permissions to "execute any command"?

Let's add our user to that group.
```plain
usermod -a -G sudo baduser
```

Let's verify that the group information looks correct for our user.

```plain
grep baduser /etc/group
```

Verify sudo permisions that exist for baduser
```plain
sudo -l -U baduser
```

Let's wait another 60 seconds and see if the logs are showing better output for our user.

```plain
sleep 60
```

Check logs

```plain
tail -20 /var/log/auth.log
```

```plain
tail -20 /var/log/syslog
```

```plain
grep baduser /var/log/*
```

What values are you seeing now in there, in regards to the baduser account and sudo access?

Is the user now successfully performing their sudo commands? Why or why not?

If you want to fix their new 'sudo auth' issue, you have to give baduser a password of 1234. the password MUST be 1234.

```plain
passwd baduser
```

</details>