# plumbing

**Description:**

Sometimes you need to handle process data outside of a file. Can you find a way to keep the output from this program and search for the flag? Connect to
> jupiter.challenges.picoctf.org 7480

>Hint: What's a pipe? No not that kind of pipe... This [kind](http://www.linfo.org/pipes.html)


Use netcat `nc` to connect to `jupiter.challenges.picoctf.org 7480`.
You will see a large wall of text. Instead of manually searching this text, we can use grep to find the flag using the standard flag format starting with 'picoCTF{'

```bash
nc jupiter.challenges.picoctf.org 7480 | grep 'picoCTF'
```

This will output the flag.
