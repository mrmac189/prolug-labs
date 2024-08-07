Detatch from screen session and verify it is still there

Reconnect and then kill the session

Create a new screen session with logging enabled to /root/screenlog.log

<br>

### Solution


Detatch from screen session

```plain
Ctrl A + D D
```

Verify that screen session is still running

```plain
screen -ls
```

Reconnect to that session

```plain
screen -r
```

Kill each window sessions

```plain
Ctrl A + K
y    #To really kill the window
```

Create a screen session with logging enabled to /root/screenlog.log

```plain
screen -L -Logfile /root/screenlog.log
```

Execute a command to log it out

```plain
for i in $(seq 100); do uptime; sleep 1; done
```

Detach the screen

```plain
Ctrl A + D D
```

Check log file
```plain
cat /root/screenlog.log
```


