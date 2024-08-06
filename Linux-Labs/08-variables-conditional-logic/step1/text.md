You are a new system administrator at a company. You've decided that you need to start gathering system information so you can use it in scripts. You know that this will give you more capabilities for automation and collection of system state.

Check your bash environment variables

Create some variables with system data

Output those variables to the screen

<br>

### Solution
<details>
<summary>Solution</summary>
Check your environmental variables

```plain
printenv
```

Also

```plain
env
```

and also 

```plain
declare -p
```

and also 

```plain
set
```
---
Is there any difference between the two above commands? How can you prove it?

We can check the difference with: 
```plain
printenv | wc -l
env | wc -l
declare -p | wc -l
set | wc -l
```
- `set` gives us more lines, it will include all env vars, shell vars and functions
- `declare -p` gives as a little less lines, it will include all env vars and shell vars
- `printenv` and `env` are quite the same and will give us only env vars
---
Test the output of a variable named `$name`

```plain
echo $name
```

Did that give any output, why or why not?
- It doesn't exist.

Let's populate that variable with some information

```plain
uname
name=$(uname)
```

Test the output of a variable named `$name`

```plain
echo $name
```

Can you capture whether or not processes are running? Test for httpd and sshd.

```plain
ps -ef | grep -i [h]ttpd
httpdCheck=$(echo $?)
```

```plain
ps -ef | grep -i [s]shd
sshdCheck=$(echo $?)
```

Can you verify that they're correct? Which one is running and which one is not running?

(httpd is not running and sshd is running)




</details>