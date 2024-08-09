Now let's dig a little deeper

Do each command and think about what output you're looking at. You may run them multiple times, if needed and to compare the output.


### Solution

#### Virtual memory usage
Let's look at the virtual memory usage of this system.

```plain
vmstat 1 5
```

What are you seeing here? Is this system under high memory usage or not?

- `vmstat` command with `delay` and `count` parameters show virtual memory usage. It would be better to use also `-S m` to show info in megabytes.
- short said, virtual memory is RAM + swap combined together as OS abstraction for processes
	- `free -h` shows how much memory is free in a simple manner  
- System is not under high memory usage.

Output:
```plain
# vmstat 1 5 -S m

procs -----------memory---------- ---swap-- -----io---- -system-- ------cpu-----
r  b   swpd   free   buff  cache   si   so    bi    bo   in   cs us sy id wa st
... 
0  0      0    254    115   1357    0    0   174   146   77  193  1  0 98  0  0
```

- **procs**:
    - `r` (run queue): 0 - Number of processes waiting for CPU time. 
    - `b` (blocked): 0 - Number of processes in uninterruptible sleep (waiting for an I/O operation to complete) 
- **memory**:
    - `swpd` (swap used): 0 - No swap space is in use. 
    - `free` (free memory): 254 MB - The amount of free physical RAM available. 
    - `buff` (buffer memory): 115 MB - Memory used for buffering I/O operations.
    - `cache` (cache memory): 1357 MB - Memory used for caching files and other data, system is making good use of available memory to speed up access to frequently used data.
- **swap**:
    - `si` (swap in): 0 – No data is being swapped in from disk. 
    - `so` (swap out): 0 – No data is being swapped out to disk. 
- **io**:
    - `bi` (blocks in): 180 - The number of blocks read from the disk per second. This is a low value, suggesting that disk reads are not a performance bottleneck.
    - `bo` (blocks out): 151 - The number of blocks written to the disk per second. This is also low, indicating that disk writes are not causing significant I/O wait times.
- **system**:
    - `in` (interrupts): 78 - The number of interrupts per second. 
	    - Interrupts are signals sent to the CPU to indicate that an event requires immediate attention
    - `cs` (context switches): 193 - The number of context switches per second. 
	    - Context switches occur when the CPU switches from executing one process to another. He saves the state of the current process and loads the state of the next process to be executed
- **cpu**:
    - `us` (user time): 1% - Percentage of CPU time spent executing user processes. 
    - `sy` (system time): 0% - Percentage of CPU time spent on system (kernel) processes. 
    - `id` (idle time): 98% - Percentage of CPU time spent idle. This is high, indicating that the CPU is mostly idle (awaits).
    - `wa` (waiting time): 0% - Percentage of CPU time spent waiting for I/O operations. Its not idle. Waiting happens during a time of CPUs workload.
    - `st` (steal time): 0% - Percentage of CPU time stolen from a virtual machine by the hypervisor. 
	    - This is not applicable in a non-virtualized environment but would indicate virtualization overhead if present (the problem of many VMs taking resources from each other).




#### CPU usage
Next we check the overall CPU usage of the system every second for 5 seconds.

```plain
mpstat 1 5
```
- `mpstat`  outputs activities for each available processor, processor 0 being the first one,  with `delay` and `count` parameters in that case. 

Is this system under high CPU load or not? 
- System is not under high load, but it can be seen, that hypervisor steals some CPU time from VM, however it doesn't really matter since idle is almost 100%. 

```plain
# mpstat 1 5
Linux 5.4.0-131-generic (ubuntu)        08/09/24        _x86_64_        (1 CPU)

1:00:31     CPU    %usr   %nice    %sys %iowait    %irq   %soft  %steal  %guest  %gnice   %idle
1:00:32     all    0.00    0.00    0.00    0.00    0.00    0.00    1.96    0.00    0.00   98.04
...
1:00:35     all    0.00    0.00    0.00    0.00    0.00    0.00    6.67    0.00    0.00   93.33
Average:     all    0.00    0.00    0.19    0.00    0.00    0.00    3.11    0.00    0.00   96.69
```
- **CPU**: The CPU being reported on. "all" means aggregated values for all CPUs.
- **%usr**: Percentage of CPU utilization that occurred while executing at the user level (application).
- **%nice**: Percentage of CPU utilization that occurred while executing at the user level with nice priority.
	- the more nicer process is, the more kindly he gives his resources to others, niceness can value from -20 til 19
- **%sys**: Percentage of CPU utilization that occurred while executing at the system level (kernel).
- **%iowait**: Percentage of time the CPU was idle during which the system awaited disk I/O request.
- **%irq**: Percentage of time spent servicing hardware interrupts.
	- Signals sent to the CPU by hardware devices, such as keyboards.
		- For example: when a key is pressed, a signal is sent to the CPU to process the it.
- **%soft**: Percentage of time spent servicing software interrupts.
	- Can be system calls, exceptions from some software.
- **%steal**: Percentage of time spent in involuntary wait by the virtual CPU or CPUs while the hypervisor was servicing another virtual processor.
	- Average steal is 3.11, that suggests some resource contention in the virtualized environment 
- **%guest**: Percentage of time spent running a virtual CPU for guest operating systems.
- **%gnice**: Percentage of time spent running a niced guest.
- **%idle**: Percentage of time the CPU or CPUs were idle and the system did not have an outstanding disk I/O request.


#### Running processes
Next we check what processes are running on the system

```plain
ps -ef
ps -ef | awk '{print $1}' | sort | uniq -c
```

What users is using the most processes? Do you think this system is doing any real work or just sitting there running an OS?

Next we check what processes are executing on the processor every second.

```plain
pidstat 1 5
```

Why do these have different length output? What processes were using the most CPU? Which showed up the most often?

#### Disk usage
Next we may want to see more CPU and Disk usage on the system in 1 second increments. Do you think you could modify this to run for 30 seconds?

```plain
iostat -xz 1 5
```

