Tmux session detachment and attachment, killing tmux sessions.

Creating new tmux sessions

Creating logs for panes within windows to /root/logs-tmux.log

Leaving behind processes with tmux

<br>

### Solution
<details>
<summary>Solution</summary>

Detatch from tmux session

```plain
ctrl + b and d
```

Verify that tmux session is still running

```plain
tmux ls
```

Reconnect to that session

```plain
tmux a -t 0
```

Kill your last tmux session, and list your sessions.

```plain
tmux kill-session
```

```plain
tmux list-sessions
```

Create a new session for tmux

```plain
tmux 
```

Log the output of a pane to a file

```plain
tmux pipe-pane -o "exec cat >>$HOME/'logs-tmux.log'"
```

Execute a command that keeps on running

```plain
while true; do uptime; sleep 1; done
```

Detach the tmux session

```plain
ctrl + b and d
```

View the output associated with that pane

```plain
cat $HOME/'logs-tmux.log'
```

Attach to the last session once again and cancel the process with `ctrl+c`

```plain
tmux a
```

Close all tmux sessions

```plain
tmux kill-server
```

</details>