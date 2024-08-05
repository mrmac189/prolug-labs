
[vmstat 1 5](Linux-Labs/01-system-checking/step2/text)

What are you seeing here? Is this system under high memory usage or not?

- `vmstat` command with `delay` and `count` parameters show virtual memory usage. It would be better to user also `-S m` to show info in megabytes.


[sar -n TCP,ETCP 1 5](Linux-Labs/01-system-checking/step3/text)

Do we appear to be seeing any large numbers of errors? Why might retransmits be a big problem?

- Number  of  RPC  requests  per second, those which needed to be retransmitted (for example because of a server timeout).