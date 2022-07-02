# Trivial File Transfer Protocol

## Description
Figure out how they moved the flag.
> Hint: What are some other ways to hide data?

## Solution

We are given a .pcapng, which can be opened with Wireshark. We can export the files within this capture using File > Export Objects > TFTP.

![TFTP Export](https://user-images.githubusercontent.com/45698399/176979824-1e0c83a8-1cf7-480c-82e1-5d0b50bccdfb.png)


Save all of these files locally so that you can access them from the terminal.
Starting with the `instructions.txt`, we have a string that appears to be in ROT13. Use `rot13` to decipher.

```bash
$ cat instructions.txt | rot13
TFTPDOESNTENCRYPTOURTRAFFICSOWEMUSTDISGUISEOURFLAGTRANSFER.FIGUREOUTAWAYTOHIDETHEFLAGANDIWILLCHECKBACKFORTHEPLAN
```
Let's do the same with the `plan` file.

```bash
$ cat plan | rot13
IUSEDTHEPROGRAMANDHIDITWITH-DUEDILIGENCE.CHECKOUTTHEPHOTOS
```

This seems to indicate that something was hidden in the photos. Let's run `steghide` using the password 'DUEDILIGENCE' from above.
> The file program.deb is supposed to be steghide, but you can also install it with `sudo apt install steghide` if you have trouble with the given package

```bash
$ steghide extract -sf picture1.bmp 
Enter passphrase: 
steghide: could not extract any data with that passphrase!
```

Let's repeat this on the other pictures and see if we find anything.

```bash
$ steghide extract -sf picture2.bmp 
Enter passphrase: 
steghide: could not extract any data with that passphrase!
$ steghide extract -sf picture3.bmp 
Enter passphrase: 
wrote extracted data to "flag.txt".
```

Bingo. Now we just have to read 'flag.txt' with `cat` to output the flag.


