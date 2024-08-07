Now that we've used some loops, we've decided we are going to create a script that uses both of the loop types to create 100 files on both of our servers.

Create a script that loops over a list of servers, logs into them, and then creates 100 files called /tmp/file{1..100}.

<br>

### Solution



Create a script that connects over ssh to both servers and creates the necessary files. use vi or the text editor of your choice to create this script /root/file_create.sh


```plain
#!/bin/bash

for server in $(cat /root/servers.txt)
  do ssh $server 'for i in $(seq 100); do touch /tmp/file$i; done'
done

```

Set the file to executable for root user and root group.

```plain
chmod 750 /root/file_create.sh
```

Execute the script

```plain
/root/file_create.sh
```

- My solution 1:  
`for server in $(cat /root/servers.txt); do ssh $server 'touch /tmp/file{1..100}'; done`
- My solution 2:
```bash
#!/bin/bash

servers=(node01 controlplane node02)

for server in ${servers[@]}
do
  #Using single quotes ' around the inner loop ensures that 
  #the entire command is executed on the remote server, and not expanded 
  ssh $server 'for i in $(seq 1 1 100); do touch /tmp/file$i; done'
done              
```  

If this works, you can see the files in both locations with this loop.

```plain
for server in controlplane node01; do ssh $server 'hostname;ls /tmp/file* | wc -l'; done
```

Do you see the output you expected? Why or why not?


