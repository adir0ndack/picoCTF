# advanced-potion-making

## Description
Ron just found his own copy of advanced potion making, but its been corrupted by some kind of spell. Help him recover it!

## Solution
Running `file` on the downloaded file 'advanced-potion-making' returns that it is 'data'.

Open up a hex editor to inspect the magic header. This will check if this is a corrupted file of some kind.

```bash
$ hexedit advanced-potion-making
```
We can see that this is likely a corrupted PNG file. Use [this list of file signatures](https://en.wikipedia.org/wiki/List_of_file_signatures) to find the correct PNG header.

Edit the file to match the correct file signature, and save the file.

Now when we try to open, we get this red screen:

![Screenshot from 2022-07-01 21-16-26](https://user-images.githubusercontent.com/45698399/176981346-45ad9dbc-9d62-4e7d-b351-33b12734532c.png)

There is probably data hidden in here. Use `stegsolve` to manipulate the image.

```bash
$ java -jar stegsolve.jar
```

Click through the different color profiles to reveal the flag:

![Screenshot from 2022-07-01 21-28-53](https://user-images.githubusercontent.com/45698399/176981710-b0ab6f46-52ee-4707-ac53-e7f3045f9dcd.png)




