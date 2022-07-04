# Big Zip

**Description:**

Unzip this archive and find the flag.  
> Hint: Can grep be instructed to look at every file in a directory and its subdirectories?


We are given a zip file, and prompted to use `grep` to find the flag.

Use `wget` to download the zip, and `unzip` to extract.

`cd` to the directory, and run `grep` with arguments `-nr` to search in all subdirectories for the given text.
In this case, we are searching for the standard flag format starting with 'picoCTF{'.

```bash
grep -nr 'picoCTF{'
```

This will output the file path to a .txt file, followed by the line containing the flag.

