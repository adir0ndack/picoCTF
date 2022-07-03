# File types

## Description
This file was found among some files marked confidential but my pdf reader cannot read it, maybe yours can.
> Hint: Remember that some file types can contain and nest other files

## Solution

We are given a file called 'Flag.pdf'. Obviously, we are meant to look for embedded files. First, we should check what kind of file this actually is.

```bash
$ file Flag.pdf
Flag.pdf: shell archive text
```

We get our first hint about the nature of the nested files here. My first instinct was to run `binwalk`.

```bash
$ binwalk -eM Flag.pdf
DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             Executable script, shebang: "/bin/sh"
168           0xA8            Executable script, shebang: "/bin/sh' line above, then type 'sh FILE'."
3029          0xBD5           uuencoded data, file name: "flag", file permissions: "600"
```

Ah. We can probably just change the file extension to .sh and see what we get.

```bash
$ cp Flag.pdf Flag.sh
$ chmod +x Flag.sh
$ ./Flag.sh
x - created lock directory _sh00046.
x - extracting flag (text)
x - removed lock directory _sh00046.
```

We now have a new text file, called 'flag'. Running `cat` brought back jibberish, so I checked `file flag` to reveal that it was an ar archive.

Let's run binwalk on this file.

```bash
$ binwalk -e flag 

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
100           0x64            bzip2 compressed data, block size = 900k

$ cd _flag.extracted/
$ ls
64
```

We now have yet another new file, called 64. This is a gzip file. I extracted this as well, and ended up with an lzip.

Run `lzip` on the new 'flag' with `lzip -d -k flag` to reveal another file called 'flag.out'.

This ends up being an LZ4 file, extracted with `lz4 -d flag.out flag2.out`. You must specify an output file.

Following the same pattern as before (checking file type, extracting, and checking the output), I extracted this series (it becomes quite a rabbit hole):

```bash
$ file flag2.out
flag2.out: LZMA compressed data, non-streamed, size 254
$ cp flag2.out flag2.lzma
$ lzma -d -k flag2.lzma
$ ls
flag  flag2  flag2.lzma  flag2.out  flag.gz  flag.out
$ file flag2
flag2: lzop compressed data - version 1.040, LZO1X-1, os: Unix
$ cp flag2 flag2.lzop
$ lzop -d -k flag2.lzop -o flag3
$ ls
flag  flag2  flag2.lzma  flag2.lzop  flag2.out  flag3  flag.gz  flag.out
$ file flag3
flag3: lzip compressed data, version: 1
$ lzip -d -k flag3
$ ls
flag  flag2  flag2.lzma  flag2.lzop  flag2.out  flag3  flag3.out  flag.gz  flag.out
$ file flag3.out
flag3.out: XZ compressed data
$ cp flag3.out flag4.xz
$ xz -d -k flag4.xz
$ ls
flag   flag2.lzma  flag2.out  flag3.out  flag4     flag.gz
flag2  flag2.lzop  flag3      flag3.xz   flag4.xz  flag.out
$ file flag4
flag4: ASCII text
$ cat flag4
7069636f4354467b66316c656e406d335f6d406e3170756c407431306e5f
6630725f3062326375723137795f37396230316332367d0a
```

Finally, we end up with a file that is ASCII text. We can make this readable using `xxd`.

```bash
$ cat flag4 | xxd -r -p
```
This will output the flag.

