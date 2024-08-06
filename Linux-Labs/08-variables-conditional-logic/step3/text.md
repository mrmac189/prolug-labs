Now that you've done some basic decision logic, let's add in inclusive "or" and exclusive "and" to the equation.

<br>

### Solution
<details>
<summary>Solution</summary>

Add in a check that checks for both sshd to be on and httpd to be off.

```plain
if [ $httpdCheck -eq "1" -a $sshdCheck -eq "0" ]; then echo "This system is good"; fi
```
Another approach with Bash syntax, operators  `&&` for AND and `||` for OR can be used:
- `if [[ httpdCheck -eq 1 ]] && [[ sshdCheck -eq 0 ]]; then echo "OK"; else echo "ERROR"; fi`

If that comes out with your expected output, then break it and see if both of them have to be true. (They do)


Now we'll try it with "or" logic and see that behavior

```plain
if [ $httpdCheck -eq "1" -o $sshdCheck -eq "1" ]; then echo "This system is good"; fi
```

Can you break this one? Does it matter if one or the other is true, or does only one have to be true for this to evaluate to true? (Only one is needed in the inclusive "or")

</details>